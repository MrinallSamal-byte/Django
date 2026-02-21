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
  - [The Admin Site](#the-admin-site)
  - [Sessions Framework](#sessions-framework)
  - [Messages Framework](#messages-framework)
  - [Context Processors](#context-processors)
- [Part 4: Models &amp; Databases](#part-4-models--databases)
  - [Defining Models](#defining-models)
  - [Field Types and Options](#field-types-and-options)
  - [Relationships](#relationships)
  - [Migrations](#migrations)
  - [QuerySet API](#queryset-api)
  - [Raw SQL and Database Functions](#raw-sql-and-database-functions)
  - [Model Inheritance](#model-inheritance)
  - [Custom Model Fields](#custom-model-fields)
  - [Generic Relations and the ContentTypes Framework](#generic-relations-and-the-contenttypes-framework)
  - [Fixtures](#fixtures)
- [Part 5: Views &amp; Templates](#part-5-views--templates)
  - [Function-Based Views](#function-based-views)
  - [Class-Based Views](#class-based-views)
  - [Template Language](#template-language)
  - [Template Inheritance](#template-inheritance)
  - [Static Files and Media](#static-files-and-media)
  - [Canonical URLs for Models](#canonical-urls-for-models)
  - [SEO-Friendly URLs](#seo-friendly-urls)
  - [Custom Template Tags and Filters](#custom-template-tags-and-filters)
  - [Class-Based View Mixins](#class-based-view-mixins)
- [Part 6: Forms &amp; User Input](#part-6-forms--user-input)
  - [Django Forms](#django-forms)
  - [ModelForms](#modelforms)
  - [Validation](#validation)
  - [File Uploads](#file-uploads)
  - [Formsets](#formsets)
  - [Cleaning Form Fields](#cleaning-form-fields)
- [Part 7: Authentication &amp; Security](#part-7-authentication--security)
  - [User Authentication](#user-authentication)
  - [Permissions and Groups](#permissions-and-groups)
  - [CSRF, XSS, and SQL Injection Protection](#csrf-xss-and-sql-injection-protection)
  - [HTTPS and Security Middleware](#https-and-security-middleware)
  - [Built-in Authentication Views](#built-in-authentication-views)
  - [User Profiles and Extending the User Model](#user-profiles-and-extending-the-user-model)
  - [Custom Authentication Backends](#custom-authentication-backends)
  - [Social Authentication](#social-authentication)
- [Part 8: Performance Optimization](#part-8-performance-optimization)
  - [Database Query Optimization](#database-query-optimization)
  - [Caching](#caching)
  - [Pagination](#pagination)
  - [Database Indexing](#database-indexing)
  - [Redis](#redis)
  - [Memcached](#memcached)
  - [Cache Levels](#cache-levels)
  - [Django Debug Toolbar](#django-debug-toolbar)
- [Part 9: Advanced Features](#part-9-advanced-features)
  - [Django REST Framework](#django-rest-framework)
  - [Signals](#signals)
  - [Custom Management Commands](#custom-management-commands)
  - [Middleware](#middleware)
  - [Celery and Async Tasks](#celery-and-async-tasks)
  - [Internationalization](#internationalization)
    - [Rosetta Translation Interface](#rosetta-translation-interface)
    - [Translating Models with django-parler](#translating-models-with-django-parler)
    - [Format Localization](#format-localization)
    - [Validating Form Fields with django-localflavor](#validating-form-fields-with-django-localflavor)
    - [URL Patterns for Internationalization](#url-patterns-for-internationalization)
  - [Sitemaps](#sitemaps)
  - [RSS Feeds](#rss-feeds)
  - [Full-Text Search](#full-text-search)
  - [Sending Emails](#sending-emails)
  - [PDF Generation](#pdf-generation)
  - [CSV Export](#csv-export)
  - [Payment Integration (Stripe)](#payment-integration-stripe)
  - [Tagging with django-taggit](#tagging-with-django-taggit)
  - [Image Handling and Thumbnails](#image-handling-and-thumbnails)
  - [Django Channels and WebSockets](#django-channels-and-websockets)
  - [Building a Follow System](#building-a-follow-system)
  - [Asynchronous JavaScript with Django](#asynchronous-javascript-with-django)
  - [Coupon System](#coupon-system)
  - [Recommendation Engine](#recommendation-engine)
  - [Extending the Admin Site](#extending-the-admin-site)
- [Part 10: Real-World Projects &amp; Deployment](#part-10-real-world-projects--deployment)
  - [Project: Task Manager](#project-task-manager)
  - [Project: Blog Platform](#project-blog-platform)
  - [Project: E-Commerce Store](#project-e-commerce-store)
  - [Deploying with Gunicorn and Nginx](#deploying-with-gunicorn-and-nginx)
  - [Docker Deployment](#docker-deployment)
  - [Managing Settings for Multiple Environments](#managing-settings-for-multiple-environments)
  - [Docker Compose in Depth](#docker-compose-in-depth)
  - [Serving Django with uWSGI and NGINX](#serving-django-with-uwsgi-and-nginx)
  - [SSL/TLS Certificates](#ssltls-certificates)
  - [Serving Django Channels with Daphne](#serving-django-channels-with-daphne)
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
# Linux / macOS
python3 --version          # Expected: Python 3.8 or higher

# Windows (Command Prompt or PowerShell)
python --version           # Expected: Python 3.8 or higher

# On Ubuntu/Debian, install if missing
sudo apt update && sudo apt install python3 python3-pip python3-venv

# On macOS (using Homebrew)
brew install python

# On Windows — download the installer from https://www.python.org/downloads/
# and check "Add Python to PATH" during installation
```

### Setting Up a Virtual Environment

1️⃣ **WHY** — Virtual environments isolate project dependencies, preventing conflicts between projects that require different package versions.

2️⃣ **WHEN** — Always — create one for every new Django project.

3️⃣ **HOW**

```bash
# Create a virtual environment named 'venv'
# Linux / macOS
python3 -m venv venv

# Windows
python -m venv venv

#   -m venv  → invoke the venv module
#   venv     → directory name for the environment

# Activate the environment
source venv/bin/activate        # Linux / macOS
venv\Scripts\activate           # Windows (Command Prompt)
venv\Scripts\Activate.ps1       # Windows (PowerShell)

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


### The Admin Site

> 💡 **Analogy:** The Django admin is like a **back-office control room** in a warehouse. You do not need to build dashboards from scratch — Django generates one automatically from your models. You just tell it which models to monitor and how to display them.

1️⃣ **WHY** — Django provides a production-ready administration interface out of the box. Instead of writing CRUD pages by hand for every model, you register models with the admin and get a full management UI — complete with search, filtering, sorting, and bulk actions — for free.

2️⃣ **WHEN** — Use the admin site whenever you need to manage data behind the scenes: adding blog posts, moderating users, reviewing orders, or populating product catalogs. It is ideal for internal tools and content management workflows.

3️⃣ **HOW**

First, create a superuser account:

```bash
python manage.py createsuperuser
#   createsuperuser → prompts for username, email, and password
#   This account has full access to the admin site at /admin/
```

Register a model with the admin in its simplest form:

```python
# blog/admin.py
from django.contrib import admin
from .models import Post, Category

admin.site.register(Category)
#   register() → makes the Category model visible in the admin
#   Django generates list, add, change, and delete views automatically
```

Customize the admin display with a `ModelAdmin` class:

```python
# blog/admin.py
from django.contrib import admin
from .models import Post, Category

@admin.register(Post)
#   @admin.register → decorator shortcut for admin.site.register(Post, PostAdmin)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'slug', 'category', 'status', 'publish_date']
    #   list_display → columns shown on the changelist page

    list_filter = ['status', 'publish_date', 'category']
    #   list_filter → sidebar filters for narrowing results

    search_fields = ['title', 'body']
    #   search_fields → enables a search box; searches these fields

    ordering = ['-publish_date']
    #   ordering → default sort order in the admin list

    prepopulated_fields = {'slug': ('title',)}
    #   prepopulated_fields → auto-fills slug from title via JavaScript

    date_hierarchy = 'publish_date'
    #   date_hierarchy → adds date-based drill-down navigation at the top

    readonly_fields = ['created_at', 'updated_at']
    #   readonly_fields → displayed but not editable

    list_editable = ['status']
    #   list_editable → allows editing status directly on the list page
    #   Note: a field in list_editable must also be in list_display
    #         and must NOT be the first field in list_display
```

Show facet counts on filters (Django 5.0+):

```python
@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_filter = ['status', 'category']
    show_facets = admin.ShowFacets.ALWAYS
    #   show_facets → displays the count of objects next to each filter value
    #   Options:
    #     ShowFacets.ALWAYS  → always show counts (e.g., "Published (12)")
    #     ShowFacets.ALLOW   → show counts only when ?_facets is in the URL
    #     ShowFacets.NEVER   → never show counts (default)
```

Use inline model admins to edit related objects on the same page:

```python
# blog/admin.py
from django.contrib import admin
from .models import Post, Comment

class CommentInline(admin.TabularInline):
    #   TabularInline → displays related objects in a compact table layout
    #   Use admin.StackedInline for a vertical, form-style layout instead
    model = Comment
    #   model → the related model to display inline

    extra = 1
    #   extra → number of empty forms to show for adding new comments

    readonly_fields = ['author', 'created_at']
    #   readonly_fields → prevent editing these fields inline


@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'status', 'publish_date']
    inlines = [CommentInline]
    #   inlines → list of inline classes; comments appear on the post edit page
```

Define custom admin actions for bulk operations:

```python
# blog/admin.py
from django.contrib import admin
from .models import Post

@admin.action(description='Mark selected posts as published')
#   @admin.action → decorator that sets the action's display name
def make_published(modeladmin, request, queryset):
    #   modeladmin → the current ModelAdmin instance
    #   request    → the current HTTP request
    #   queryset   → the selected objects from the changelist
    queryset.update(status='published')
    #   update()   → bulk-updates all selected rows in a single SQL query


@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'status', 'publish_date']
    actions = [make_published]
    #   actions → list of custom actions available in the action dropdown
```

### Sessions Framework

> 💡 **Analogy:** A session is like a **coat-check ticket** at a theater. The theater (server) stores your coat (data) and gives you a ticket (session ID cookie). Each time you return with the ticket, the theater retrieves your coat — you never carry it yourself.

1️⃣ **WHY** — HTTP is stateless — each request is independent. Sessions let you store data for a specific visitor across multiple requests. Without sessions, features like shopping carts, login state, and user preferences would be impossible.

2️⃣ **WHEN** — Use sessions to persist per-user data between page loads: shopping carts, recently viewed items, multi-step form wizards, language preferences, or any transient data that should not live in the database permanently.

3️⃣ **HOW**

Django sessions require `django.contrib.sessions` in `INSTALLED_APPS` and the session middleware (both included by default):

```python
# settings.py — session configuration

INSTALLED_APPS = [
    # ...
    'django.contrib.sessions',
    #   Provides the session framework and database backend
]

MIDDLEWARE = [
    # ...
    'django.contrib.sessions.middleware.SessionMiddleware',
    #   Manages session cookies and attaches request.session
]
```

Configure the session backend in `settings.py`:

```python
# settings.py — session backend options

SESSION_ENGINE = 'django.contrib.sessions.backends.db'
#   SESSION_ENGINE → controls where session data is stored
#   Options:
#     'django.contrib.sessions.backends.db'       → database (default)
#     'django.contrib.sessions.backends.cache'     → cache only (fast, volatile)
#     'django.contrib.sessions.backends.cached_db' → cache + database fallback
#     'django.contrib.sessions.backends.file'      → server filesystem
#     'django.contrib.sessions.backends.signed_cookies' → signed browser cookies

SESSION_COOKIE_AGE = 1209600
#   SESSION_COOKIE_AGE → session lifetime in seconds (default: 1209600 = 2 weeks)

SESSION_EXPIRE_AT_BROWSER_CLOSE = False
#   False → session persists after browser is closed (until cookie expires)
#   True  → session cookie is deleted when the browser closes

SESSION_SAVE_EVERY_REQUEST = True
#   True  → update the session expiry on every request (sliding window)
#   False → only save when the session is modified (default)
```

Read and write session data in views:

```python
# shop/views.py
from django.shortcuts import render

def set_favorite(request):
    """Store a user preference in the session."""
    request.session['favorite_color'] = 'blue'
    #   request.session → dict-like object for the current user's session
    #   Assignment automatically marks the session as modified and saves it

    return render(request, 'shop/preference_saved.html')


def get_favorite(request):
    """Read a value from the session."""
    color = request.session.get('favorite_color', 'not set')
    #   .get(key, default) → safe access; returns default if key is missing

    return render(request, 'shop/show_favorite.html', {'color': color})


def clear_session(request):
    """Remove specific data or flush the entire session."""
    del request.session['favorite_color']
    #   del → removes a single key from the session

    # Or flush everything:
    # request.session.flush()
    #   flush() → deletes the session data and regenerates the session key

    return render(request, 'shop/session_cleared.html')
```

Store shopping cart data in the session:

```python
# cart/cart.py
from decimal import Decimal
from django.conf import settings
from shop.models import Product

class Cart:
    def __init__(self, request):
        self.session = request.session
        #   Store a reference to the current session

        cart = self.session.get(settings.CART_SESSION_ID)
        #   Retrieve the cart dict from the session (or None)

        if not cart:
            cart = self.session[settings.CART_SESSION_ID] = {}
            #   Initialize an empty cart dict in the session

        self.cart = cart

    def add(self, product, quantity=1, override_quantity=False):
        """Add a product to the cart or update its quantity."""
        product_id = str(product.id)
        #   Session keys must be strings (JSON serialization)

        if product_id not in self.cart:
            self.cart[product_id] = {
                'quantity': 0,
                'price': str(product.price),
                #   Store price as string to avoid Decimal serialization issues
            }

        if override_quantity:
            self.cart[product_id]['quantity'] = quantity
        else:
            self.cart[product_id]['quantity'] += quantity

        self.save()

    def remove(self, product):
        """Remove a product from the cart."""
        product_id = str(product.id)
        if product_id in self.cart:
            del self.cart[product_id]
            self.save()

    def save(self):
        """Mark the session as modified so Django saves it."""
        self.session.modified = True
        #   modified = True → forces Django to write session data to the backend
        #   Needed when you mutate a nested object instead of assigning a key

    def get_total_price(self):
        """Calculate the total cost of all items in the cart."""
        return sum(
            Decimal(item['price']) * item['quantity']
            for item in self.cart.values()
        )

    def clear(self):
        """Remove the entire cart from the session."""
        del self.session[settings.CART_SESSION_ID]
        self.save()
```

Add the cart session key to settings:

```python
# settings.py
CART_SESSION_ID = 'cart'
#   CART_SESSION_ID → the key used to store cart data in request.session
```

### Messages Framework

> 💡 **Analogy:** The messages framework is like a **sticky note system** in an office. After completing a task (processing a form), you stick a note ("Order placed successfully!") on the door for the next person who walks in (the next page load). Once they read it, the note is removed.

1️⃣ **WHY** — Web applications need to show one-time notifications to users after actions like submitting a form, logging in, or encountering an error. The messages framework provides a simple, cookie-based mechanism for passing these notifications between requests.

2️⃣ **WHEN** — Use messages whenever you redirect after a POST and need to inform the user of the result: success confirmations, validation warnings, error alerts, or informational notices.

3️⃣ **HOW**

The messages framework is enabled by default. It requires these entries in `settings.py`:

```python
# settings.py — messages framework requirements (included by default)

INSTALLED_APPS = [
    # ...
    'django.contrib.messages',
    #   Provides the messages storage backend
]

MIDDLEWARE = [
    # ...
    'django.contrib.sessions.middleware.SessionMiddleware',
    #   Messages depend on sessions to persist between requests
    'django.contrib.messages.middleware.MessageMiddleware',
    #   Attaches the messages storage to each request
]

TEMPLATES = [
    {
        'OPTIONS': {
            'context_processors': [
                # ...
                'django.contrib.messages.context_processors.messages',
                #   Makes the 'messages' variable available in all templates
            ],
        },
    },
]
```

Add messages in views:

```python
# shop/views.py
from django.contrib import messages
from django.shortcuts import redirect, render
from .forms import OrderForm

def create_order(request):
    if request.method == 'POST':
        form = OrderForm(request.POST)
        if form.is_valid():
            form.save()

            messages.success(request, 'Your order was placed successfully!')
            #   messages.success() → adds a SUCCESS-level message
            #   The message is stored in the session and displayed on the next page

            return redirect('shop:order_complete')

        messages.error(request, 'Please correct the errors below.')
        #   messages.error() → adds an ERROR-level message

    else:
        form = OrderForm()

    return render(request, 'shop/create_order.html', {'form': form})
```

All available message levels:

```python
from django.contrib import messages

messages.debug(request, 'Debug: SQL query took 23ms')
#   DEBUG   → low-level information for development (hidden by default)

messages.info(request, 'Your account settings have been updated.')
#   INFO    → general informational message

messages.success(request, 'Product added to cart!')
#   SUCCESS → action completed successfully

messages.warning(request, 'Your trial expires in 3 days.')
#   WARNING → something requires attention but is not an error

messages.error(request, 'Payment failed. Please try again.')
#   ERROR   → an action failed or something went wrong
```

Display messages in templates:

```html
<!-- templates/base.html -->
{% if messages %}
<div class="messages">
    {% for message in messages %}
    <div class="alert alert-{{ message.tags }}" role="alert">
        {# message.tags → space-separated CSS classes like "success" or "error" #}
        {# Maps to Bootstrap: alert-success, alert-warning, alert-danger, etc. #}
        {{ message }}
    </div>
    {% endfor %}
</div>
{% endif %}
```

Customize message tags to match CSS frameworks like Bootstrap:

```python
# settings.py
from django.contrib.messages import constants as message_constants

MESSAGE_TAGS = {
    message_constants.DEBUG: 'secondary',
    #   Maps DEBUG level to "secondary" CSS class
    message_constants.ERROR: 'danger',
    #   Maps ERROR level to "danger" (Bootstrap uses "danger" not "error")
}
```

Choose a message storage backend:

```python
# settings.py

MESSAGE_STORAGE = 'django.contrib.messages.storage.fallback.FallbackStorage'
#   MESSAGE_STORAGE → controls where messages are temporarily stored
#   Options:
#     'django.contrib.messages.storage.session.SessionStorage'
#         → stores messages in the session (requires session middleware)
#     'django.contrib.messages.storage.cookie.CookieStorage'
#         → stores messages in a signed cookie (no server-side storage)
#     'django.contrib.messages.storage.fallback.FallbackStorage'
#         → tries cookie first, falls back to session for large messages (default)
```

### Context Processors

> 💡 **Analogy:** A context processor is like a **receptionist who hands every visitor the same welcome packet**. Instead of each office (view) preparing the packet individually, the receptionist (context processor) adds it automatically to every template rendered by the building (project).

1️⃣ **WHY** — Some data needs to be available on every page — the current user, site-wide settings, a shopping cart summary, or navigation categories. Without context processors, you would have to manually pass this data in every single view. Context processors inject variables into all templates automatically.

2️⃣ **WHEN** — Use a context processor when a variable is needed across many (or all) templates: global navigation data, cart item counts, unread notification counts, feature flags, or site configuration.

3️⃣ **HOW**

Django includes several built-in context processors (configured by default):

```python
# settings.py — default context processors
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                #   Adds 'debug' (bool) and 'sql_queries' to templates

                'django.template.context_processors.request',
                #   Adds 'request' — the current HttpRequest object

                'django.contrib.auth.context_processors.auth',
                #   Adds 'user' (current user) and 'perms' (permissions)

                'django.contrib.messages.context_processors.messages',
                #   Adds 'messages' — the list of pending user messages
            ],
        },
    },
]
```

Write a custom context processor to make cart data available globally:

```python
# cart/context_processors.py
from .cart import Cart

def cart(request):
    """Make the shopping cart available in every template."""
    return {'cart': Cart(request)}
    #   Returns a dict — each key becomes a template variable
    #   The Cart object is initialized from the current session
    #   Now {{ cart.get_total_price }} and {{ cart|length }} work everywhere
```

A context processor is simply a function that takes a `request` and returns a `dict`:

```python
# shop/context_processors.py
from .models import Category

def categories(request):
    """Make all product categories available for site-wide navigation."""
    return {
        'categories': Category.objects.all(),
        #   Every template can now loop over {{ categories }}
    }
```

Register your custom context processors in `settings.py`:

```python
# settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
                'cart.context_processors.cart',
                #   ← custom: injects 'cart' into every template context
                'shop.context_processors.categories',
                #   ← custom: injects 'categories' into every template context
            ],
        },
    },
]
```

Use the injected variables in any template without passing them from views:

```html
<!-- templates/base.html -->
<nav>
    {% for category in categories %}
        {# 'categories' comes from the context processor, not the view #}
        <a href="{{ category.get_absolute_url }}">{{ category.name }}</a>
    {% endfor %}
</nav>

<div class="cart-summary">
    Cart total: ${{ cart.get_total_price }}
    {# 'cart' comes from cart.context_processors.cart #}
</div>
```

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


### Model Inheritance

> 💡 **Analogy:** Model inheritance is like **building with LEGO base plates**. An abstract model is a base plate you never display on its own — it only provides a foundation for other builds. Multi-table inheritance is two separate display models connected by a hinge. A proxy model is putting a different minifigure on the exact same build — same structure, different behavior.

1️⃣ **WHY** — Model inheritance lets you reuse common fields and logic across multiple models, reducing duplication. Django supports three distinct strategies, each with different database implications: abstract models share fields without creating a table, multi-table inheritance creates a linked table per model, and proxy models change Python-level behavior without touching the schema.

2️⃣ **WHEN** — Use abstract models when several models share the same fields (e.g., timestamps). Use multi-table inheritance when you have a true "is-a" relationship and need to query the parent independently. Use proxy models when you only need a different default ordering, manager, or method set on an existing table.

3️⃣ **HOW**

#### Abstract Models

An abstract model is a base class that contributes fields to its children but **never creates its own database table**.

```python
# core/models.py
from django.db import models
from django.utils import timezone


class TimeStampedModel(models.Model):
    """Reusable base that adds created/updated timestamps."""
    created_at = models.DateTimeField(auto_now_add=True)
    #   auto_now_add=True → set once when the row is first inserted
    updated_at = models.DateTimeField(auto_now=True)
    #   auto_now=True     → refreshed every time .save() is called

    class Meta:
        abstract = True
        #   abstract=True → Django will NOT create a 'core_timestampedmodel' table
        #   Child models inherit created_at and updated_at into their own tables


# blog/models.py
from core.models import TimeStampedModel


class Post(TimeStampedModel):
    title = models.CharField(max_length=200)
    #   title lives in the blog_post table alongside created_at and updated_at
    body = models.TextField()

    def __str__(self):
        return self.title


class Comment(TimeStampedModel):
    post = models.ForeignKey(Post, on_delete=models.CASCADE, related_name='comments')
    #   ForeignKey → many-to-one; each comment belongs to one post
    text = models.TextField()

    def __str__(self):
        return f'Comment on {self.post.title}'

# Result:
#   blog_post    → id, title, body, created_at, updated_at
#   blog_comment → id, post_id, text, created_at, updated_at
#   No table is created for TimeStampedModel itself
```

#### Multi-Table Inheritance

Each model in the hierarchy gets its **own database table**, linked by an automatic `OneToOneField`.

```python
# directory/models.py
from django.db import models


class Place(models.Model):
    name = models.CharField(max_length=100)
    #   name lives in directory_place
    address = models.CharField(max_length=200)

    def __str__(self):
        return self.name


class Restaurant(Place):
    serves_pizza = models.BooleanField(default=False)
    #   serves_pizza lives in directory_restaurant
    serves_pasta = models.BooleanField(default=False)

    def __str__(self):
        return f'{self.name} (Restaurant)'

# Result:
#   directory_place      → id, name, address
#   directory_restaurant → place_ptr_id (PK + FK to directory_place),
#                          serves_pizza, serves_pasta
#
#   Django creates an implicit OneToOneField called place_ptr
#   linking directory_restaurant back to directory_place.
```

```python
# Querying multi-table inheritance
from directory.models import Place, Restaurant

# Create a restaurant — a row is inserted into BOTH tables
restaurant = Restaurant.objects.create(
    name='Bella Napoli',
    address='123 Main St',
    serves_pizza=True,
    serves_pasta=True,
)
#   INSERT INTO directory_place (name, address) VALUES (...)
#   INSERT INTO directory_restaurant (place_ptr_id, serves_pizza, serves_pasta) VALUES (...)

# Query from the parent — returns all places, including restaurants
Place.objects.all()
#   SELECT * FROM directory_place

# Access the child from a parent instance
place = Place.objects.get(name='Bella Napoli')
place.restaurant
#   Follows the implicit OneToOneField to fetch the Restaurant row
#   Raises Restaurant.DoesNotExist if the place is not a restaurant

# Query from the child — automatically JOINs both tables
Restaurant.objects.filter(serves_pizza=True)
#   SELECT ... FROM directory_restaurant
#   INNER JOIN directory_place ON (place_ptr_id = directory_place.id)
#   WHERE serves_pizza = 1
```

#### Proxy Models

A proxy model operates on the **same database table** as its parent but can define different Python behavior — custom managers, methods, ordering, or Meta options.

```python
# blog/models.py
from django.db import models


class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    publish_date = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['-publish_date']
        #   Default: newest first

    def __str__(self):
        return self.title


class OrderedPost(Post):
    """Proxy that orders posts alphabetically by title."""

    class Meta:
        proxy = True
        #   proxy=True → no new table is created
        #   OrderedPost reads from and writes to the same blog_post table
        ordering = ['title']
        #   Overrides the parent's ordering

    def title_upper(self):
        return self.title.upper()
        #   Extra convenience method available only on OrderedPost instances

# Usage:
#   Post.objects.all()        → ordered by -publish_date
#   OrderedPost.objects.all() → ordered by title (same table, different query)
```

---

### Custom Model Fields

> 💡 **Analogy:** Django's built-in fields are like **standard kitchen appliances** — an oven, a fridge, a microwave. A custom model field is a **purpose-built gadget** you design yourself when no standard appliance does the job, like an automatic bread slicer that always cuts to the right thickness.

1️⃣ **WHY** — Sometimes the built-in field types do not capture your domain logic. A custom field encapsulates validation, database conversion, and automatic value assignment in one reusable component. The classic example is an `OrderField` that auto-assigns sequential order values within a group.

2️⃣ **WHEN** — When you find yourself repeating the same `pre_save` / `save()` logic across models, or when you need a field that converts between a Python type and a database type in a non-standard way.

3️⃣ **HOW**

```python
# fields.py
from django.db import models
from django.core.exceptions import ObjectDoesNotExist


class OrderField(models.PositiveIntegerField):
    """
    Auto-assigns a sequential order value scoped to a related field.
    Example: ordering modules within a course, or lessons within a module.
    """

    def __init__(self, for_fields=None, *args, **kwargs):
        self.for_fields = for_fields
        #   for_fields → list of field names that define the ordering scope
        #   e.g., ['course'] means order resets per course
        super().__init__(*args, **kwargs)

    def deconstruct(self):
        name, path, args, kwargs = super().deconstruct()
        #   deconstruct() → tells Django how to serialize this field for migrations
        if self.for_fields is not None:
            kwargs['for_fields'] = self.for_fields
        return name, path, args, kwargs

    def pre_save(self, model_instance, add):
        """Called just before the field value is saved to the database."""
        if getattr(model_instance, self.attname) is None:
            #   self.attname → the name of this field on the model (e.g., 'order')
            #   If no value was explicitly set, auto-assign the next number

            try:
                qs = self.model.objects.all()
                #   Start with all objects of this model

                if self.for_fields:
                    #   Narrow the scope: only look at rows with matching field values
                    query = {
                        field: getattr(model_instance, field)
                        for field in self.for_fields
                    }
                    qs = qs.filter(**query)
                    #   e.g., Module.objects.filter(course=model_instance.course)

                last_item = qs.latest(self.attname)
                #   .latest() → SELECT ... ORDER BY `order` DESC LIMIT 1
                value = getattr(last_item, self.attname) + 1
                #   New order = highest existing order + 1

            except ObjectDoesNotExist:
                value = 0
                #   No existing items in scope — start at 0

            setattr(model_instance, self.attname, value)
            return value

        else:
            return super().pre_save(model_instance, add)
            #   If a value was explicitly provided, use the default behavior
```

```python
# courses/models.py
from django.db import models
from fields import OrderField


class Course(models.Model):
    title = models.CharField(max_length=200)

    def __str__(self):
        return self.title


class Module(models.Model):
    course = models.ForeignKey(Course, on_delete=models.CASCADE, related_name='modules')
    title = models.CharField(max_length=200)
    order = OrderField(for_fields=['course'], blank=True)
    #   OrderField scoped to 'course' → numbering resets for each course
    #   blank=True → not required in forms; auto-assigned if omitted

    class Meta:
        ordering = ['order']
        #   Modules display in their assigned order

    def __str__(self):
        return f'{self.order}. {self.title}'


class Lesson(models.Model):
    module = models.ForeignKey(Module, on_delete=models.CASCADE, related_name='lessons')
    title = models.CharField(max_length=200)
    order = OrderField(for_fields=['module'], blank=True)
    #   OrderField scoped to 'module' → numbering resets for each module

    class Meta:
        ordering = ['order']

    def __str__(self):
        return f'{self.order}. {self.title}'
```

```python
# Shell demo — auto-assignment in action
from courses.models import Course, Module

course = Course.objects.create(title='Django Masterclass')

m1 = Module.objects.create(course=course, title='Introduction')
#   order is None → pre_save auto-assigns 0
print(m1.order)
#   0

m2 = Module.objects.create(course=course, title='Models')
#   pre_save finds m1 with order=0 → assigns 1
print(m2.order)
#   1

m3 = Module.objects.create(course=course, title='Views')
print(m3.order)
#   2

# A new course starts numbering from 0 again
course2 = Course.objects.create(title='Flask Basics')
m4 = Module.objects.create(course=course2, title='Setup')
print(m4.order)
#   0  (scoped to course2, so order resets)
```

#### Other Custom Field Hooks

When building custom fields that need to convert between Python objects and database values, override these methods:

```python
# Example: a custom field that stores a comma-separated list as a Python list
from django.db import models


class CommaSeparatedListField(models.TextField):
    """Stores a Python list as a comma-separated string in MySQL."""

    def from_db_value(self, value, expression, connection):
        """Convert database value → Python object (called on every DB read)."""
        if value is None:
            return []
        return value.split(',')
        #   'red,green,blue' → ['red', 'green', 'blue']

    def get_prep_value(self, value):
        """Convert Python object → database value (called on every DB write)."""
        if not value:
            return ''
        return ','.join(value)
        #   ['red', 'green', 'blue'] → 'red,green,blue'

    def to_python(self, value):
        """Convert any input → Python object (called during deserialization/validation)."""
        if isinstance(value, list):
            return value
        if value is None:
            return []
        return value.split(',')
```

---

### Generic Relations and the ContentTypes Framework

> 💡 **Analogy:** A `ForeignKey` is like a **name badge** that says "I belong to Post #7." A `GenericForeignKey` is like a **universal badge** that says "I belong to item #7 in the Posts table" — it can also say "I belong to item #3 in the Courses table." It works with *any* model, not just one.

1️⃣ **WHY** — Sometimes you need a model that can relate to *any* other model — likes, comments, tags, or activity logs that apply across your entire application. Hard-coding a `ForeignKey` to each model creates an explosion of columns. The contenttypes framework and generic relations solve this by storing the target model's type and primary key dynamically.

2️⃣ **WHEN** — When building features that span multiple models: activity streams, tagging systems, comment engines, audit logs, or notification systems where the target object varies.

3️⃣ **HOW**

```python
# Ensure 'django.contrib.contenttypes' is in INSTALLED_APPS (it is by default)
# settings.py
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',    # ← required for generic relations
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
    'courses',
    'actions',
]
```

```python
# actions/models.py
from django.db import models
from django.contrib.contenttypes.models import ContentType
from django.contrib.contenttypes.fields import GenericForeignKey


class Activity(models.Model):
    """
    Activity stream entry that can point to ANY model instance.
    Example: "Alice published Post #5", "Bob completed Course #3".
    """
    user = models.ForeignKey(
        'auth.User',
        on_delete=models.CASCADE,
        related_name='activities',
    )
    #   The user who performed the action

    verb = models.CharField(max_length=200)
    #   Describes the action: 'published', 'completed', 'liked', etc.

    target_ct = models.ForeignKey(
        ContentType,
        on_delete=models.CASCADE,
        blank=True,
        null=True,
        related_name='target_activities',
    )
    #   target_ct → stores WHICH model the target is (e.g., blog | post)
    #   ContentType is a Django model with app_label and model fields
    #   In MySQL: a FK to the django_content_type table

    target_id = models.PositiveIntegerField(blank=True, null=True)
    #   target_id → stores the PK of the target object (e.g., 5)

    target = GenericForeignKey('target_ct', 'target_id')
    #   GenericForeignKey → combines target_ct + target_id into a single
    #   attribute that behaves like a regular FK
    #   NOT a real database column — it is a virtual field

    created = models.DateTimeField(auto_now_add=True)

    class Meta:
        ordering = ['-created']
        #   Newest activities first

    def __str__(self):
        return f'{self.user} {self.verb} {self.target}'
```

```python
# Adding a GenericRelation to a target model (reverse lookup)
# blog/models.py
from django.db import models
from django.contrib.contenttypes.fields import GenericRelation


class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    publish_date = models.DateTimeField(auto_now_add=True)

    activities = GenericRelation(
        'actions.Activity',
        content_type_field='target_ct',
        object_id_field='target_id',
        related_query_name='post',
    )
    #   GenericRelation → reverse accessor for Activity objects pointing at this Post
    #   content_type_field → name of the FK to ContentType on Activity
    #   object_id_field    → name of the PK field on Activity
    #   related_query_name → allows Activity.objects.filter(post=some_post)

    def __str__(self):
        return self.title
```

```python
# Shell demo — creating and querying generic relations
from django.contrib.auth.models import User
from django.contrib.contenttypes.models import ContentType
from blog.models import Post
from actions.models import Activity

user = User.objects.get(username='alice')
post = Post.objects.get(title='Django Masterclass')

# Create an activity targeting a Post
activity = Activity.objects.create(
    user=user,
    verb='published',
    target=post,
)
#   Django auto-populates target_ct and target_id:
#   target_ct → ContentType for blog.Post
#   target_id → post.pk
print(activity)
#   alice published Django Masterclass

# Access the target object (follows the generic FK)
print(activity.target)
#   <Post: Django Masterclass>
print(activity.target_ct)
#   <ContentType: blog | post>
print(activity.target_id)
#   1

# Reverse lookup — get all activities for a specific post
post.activities.all()
#   <QuerySet [<Activity: alice published Django Masterclass>]>

# Filter activities by target model type
post_ct = ContentType.objects.get_for_model(Post)
#   .get_for_model() → efficient lookup with built-in caching
Activity.objects.filter(target_ct=post_ct)
#   All activities that target any Post

# Filter activities targeting a specific post
Activity.objects.filter(target_ct=post_ct, target_id=post.pk)
#   All activities targeting this exact post
```

---

### Fixtures

> 💡 **Analogy:** Fixtures are like **frozen meals** for your database. You prepare the data once, freeze it into a JSON or YAML file, and reheat it anytime you need a fresh database pre-loaded with the same data — perfect for testing, demos, or initial setup.

1️⃣ **WHY** — Fixtures provide a portable, repeatable way to populate your database with initial or test data. Instead of manually creating objects through the admin or shell every time, you serialize data to a file and load it with a single command. They are especially valuable for seeding lookup tables (categories, countries, permissions) and for providing consistent test data.

2️⃣ **WHEN** — Use fixtures when you need initial data after running migrations (e.g., default categories), when writing tests that require a known database state, or when sharing a dataset across team members or environments.

3️⃣ **HOW**

#### Exporting Data with `dumpdata`

```bash
# Dump all data from the blog app to JSON
python manage.py dumpdata blog --indent 2 --output blog/fixtures/blog_data.json
#   dumpdata blog       → export all models in the blog app
#   --indent 2          → pretty-print with 2-space indentation
#   --output <path>     → write to file instead of stdout

# Dump a single model
python manage.py dumpdata blog.Category --indent 2 --output blog/fixtures/categories.json
#   blog.Category       → only export the Category model

# Dump specific records using --pks
python manage.py dumpdata blog.Post --pks 1,2,3 --indent 2 --output blog/fixtures/sample_posts.json
#   --pks 1,2,3         → only export posts with primary keys 1, 2, and 3

# Dump all apps except sessions and contenttypes (common for clean exports)
python manage.py dumpdata --exclude sessions --exclude contenttypes --indent 2 --output full_backup.json
#   --exclude <app>     → skip an entire app
```

#### Fixture File Format (JSON)

```json
[
  {
    "model": "blog.category",
    "pk": 1,
    "fields": {
      "name": "Python",
      "slug": "python"
    }
  },
  {
    "model": "blog.category",
    "pk": 2,
    "fields": {
      "name": "Django",
      "slug": "django"
    }
  },
  {
    "model": "blog.post",
    "pk": 1,
    "fields": {
      "title": "Getting Started with Django",
      "slug": "getting-started-with-django",
      "body": "Django is a high-level Python web framework...",
      "category": 2,
      "status": "published",
      "publish_date": "2026-01-15T10:00:00Z"
    }
  }
]
```

```
#   "model" → app_label.model_name in lowercase
#   "pk"    → primary key value
#   "fields" → dict of field_name: value
#   ForeignKey fields use the related object's PK (category: 2 → Category with pk=2)
#   DateTimeField uses ISO 8601 format
```

#### Loading Data with `loaddata`

```bash
# Load a fixture file
python manage.py loaddata blog/fixtures/categories.json
#   Reads the JSON file and inserts/updates rows in the database
#   Output: Installed 2 object(s) from 1 fixture(s)

# Django also searches for fixtures in each app's 'fixtures/' directory
# So you can simply use the filename:
python manage.py loaddata categories
#   Django looks for categories.json (or categories.yaml, categories.xml)
#   in every app's fixtures/ directory

# Load multiple fixtures at once
python manage.py loaddata categories sample_posts
#   Loads both files in order — categories first, then posts
#   Order matters when posts reference categories via ForeignKey
```

#### Fixture Directory Structure

```
myproject/
├── blog/
│   ├── fixtures/              # ← Django auto-discovers this directory
│   │   ├── categories.json    #   Default categories
│   │   ├── sample_posts.json  #   Sample blog posts
│   │   └── test_data.json     #   Data used in tests
│   ├── models.py
│   └── tests.py
└── courses/
    ├── fixtures/
    │   └── courses.json
    └── models.py
```

#### Using Fixtures in Tests

```python
# blog/tests.py
from django.test import TestCase
from blog.models import Post, Category


class PostTestCase(TestCase):
    fixtures = ['categories.json', 'sample_posts.json']
    #   fixtures → loaded into a test database before each test method
    #   The test database is destroyed after the test class finishes
    #   This guarantees a clean, known state for every test run

    def test_published_posts(self):
        published = Post.objects.filter(status='published')
        #   Data from sample_posts.json is available here
        self.assertTrue(published.exists())

    def test_category_count(self):
        count = Category.objects.count()
        #   Data from categories.json is available here
        self.assertEqual(count, 2)
        #   We defined 2 categories in the fixture file


class EmptyDatabaseTest(TestCase):
    """Test without fixtures — database starts empty."""

    def test_no_posts(self):
        self.assertEqual(Post.objects.count(), 0)
        #   No fixtures attribute → no pre-loaded data
```

#### YAML Fixtures (Alternative Format)

```bash
# Install PyYAML to use YAML fixtures
pip install pyyaml
#   Django auto-detects YAML format by file extension
```

```yaml
# blog/fixtures/categories.yaml
- model: blog.category
  pk: 1
  fields:
    name: Python
    slug: python

- model: blog.category
  pk: 2
  fields:
    name: Django
    slug: django
```

```bash
# Load YAML fixtures the same way
python manage.py loaddata categories.yaml
#   Works identically to JSON — Django handles the format automatically
```

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


### Canonical URLs for Models

> 💡 **Analogy:** A canonical URL is like a **permanent home address** for each record in your database. No matter how many roads lead to the same house, the address on the mailbox is the one everyone agrees on. `get_absolute_url()` is that mailbox — a single, authoritative method every part of your code can call to find the "official" path to an object.

1️⃣ **WHY** — Hard-coding URLs in templates and views is fragile. If a URL pattern changes, every link breaks. `get_absolute_url()` centralises the logic in the model itself, so templates, `redirect()`, the admin site, and third-party packages all resolve the correct URL automatically.

2️⃣ **WHEN** — Define `get_absolute_url()` on every model that has a detail page. Django's `CreateView` and `UpdateView` redirect to it by default when no `success_url` is set.

3️⃣ **HOW**

Add `get_absolute_url()` to your model:

```python
# blog/models.py
from django.db import models
from django.urls import reverse

class Post(models.Model):
    title = models.CharField(max_length=250)
    slug = models.SlugField(max_length=250, unique=True)
    body = models.TextField()
    status = models.CharField(max_length=10, default='draft')

    def get_absolute_url(self):
        #   reverse() builds a URL from a named URL pattern
        #   'blog:post_detail' → app_name:url_name
        #   kwargs → values that fill the <slug:post> capture group
        return reverse('blog:post_detail', kwargs={'post': self.slug})

    def __str__(self):
        return self.title
```

The matching URL pattern:

```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'
#   Namespace — lets you write 'blog:post_detail' instead of just 'post_detail'

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('<slug:post>/', views.post_detail, name='post_detail'),
    #   <slug:post> → captures a slug from the URL and passes it to the view
]
```

Using the canonical URL in templates:

```html
<!-- blog/templates/blog/post_list.html -->
{% for post in posts %}
    <h2>
        <a href="{{ post.get_absolute_url }}">{{ post.title }}</a>
        {# Calls model.get_absolute_url() — no hard-coded paths #}
    </h2>
{% endfor %}
```

Using the canonical URL in views with `redirect()`:

```python
# blog/views.py
from django.shortcuts import redirect, get_object_or_404
from .models import Post

def publish_post(request, pk):
    post = get_object_or_404(Post, pk=pk)
    post.status = 'published'
    post.save()

    return redirect(post)
    #   redirect() accepts a model instance
    #   It calls post.get_absolute_url() internally
    #   Equivalent to: redirect(post.get_absolute_url())
```

### SEO-Friendly URLs

> 💡 **Analogy:** Compare two house addresses: "Building 42" versus "42 Maple Street, Lakeside". The second one tells you where you are before you arrive. SEO-friendly URLs work the same way — `/blog/2025/06/15/django-slugs/` tells readers (and search engines) far more than `/blog/post/7/`.

1️⃣ **WHY** — Slugs and date-based paths improve search-engine ranking, make URLs human-readable, and help users guess content before clicking. Django's `SlugField` and `unique_for_date` option make this straightforward to implement with MySQL.

2️⃣ **WHEN** — Use slugs on any public-facing content — blog posts, product pages, articles. Add date segments when chronological context matters (news, blogs, changelogs).

3️⃣ **HOW**

Define a model with a slug and date fields:

```python
# blog/models.py
from django.db import models
from django.urls import reverse
from django.utils import timezone

class Post(models.Model):
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('published', 'Published'),
    ]

    title = models.CharField(max_length=250)

    slug = models.SlugField(max_length=250)
    #   SlugField → stores URL-safe strings (lowercase, hyphens, no spaces)
    #   Indexed by default — fast lookups in MySQL

    publish = models.DateTimeField(default=timezone.now)
    #   Publication date — used in the URL and for unique_for_date

    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='draft')
    body = models.TextField()

    class Meta:
        ordering = ['-publish']
        #   Newest first by default

    def get_absolute_url(self):
        return reverse(
            'blog:post_detail',
            args=[
                self.publish.year,
                self.publish.month,
                self.publish.day,
                self.slug,
            ],
        )
        #   Builds a date-based URL like /blog/2025/6/15/django-slugs/

    def __str__(self):
        return self.title
```

Use `unique_for_date` to enforce slug uniqueness per day:

```python
    slug = models.SlugField(max_length=250, unique_for_date='publish')
    #   unique_for_date='publish' → the slug only needs to be unique
    #   within the same publish date, not across all rows
    #   This lets two posts on different days share the same slug
```

Auto-populate the slug in the admin:

```python
# blog/admin.py
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'slug', 'status', 'publish']
    list_filter = ['status', 'publish']
    search_fields = ['title', 'body']

    prepopulated_fields = {'slug': ('title',)}
    #   prepopulated_fields → auto-generates the slug from the title
    #   as you type in the admin form (JavaScript-based, admin only)
```

Define date-based URL patterns:

```python
# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'

urlpatterns = [
    path('', views.post_list, name='post_list'),

    path(
        '<int:year>/<int:month>/<int:day>/<slug:post>/',
        views.post_detail,
        name='post_detail',
    ),
    #   Four capture groups — year, month, day, and slug
    #   Example match: /blog/2025/6/15/django-slugs/
]
```

Update the view to accept the new parameters:

```python
# blog/views.py
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    posts = Post.objects.filter(status='published')
    return render(request, 'blog/post_list.html', {'posts': posts})


def post_detail(request, year, month, day, post):
    post = get_object_or_404(
        Post,
        status='published',
        slug=post,
        publish__year=year,
        publish__month=month,
        publish__day=day,
    )
    #   Filter by date components AND slug
    #   Ensures the URL date matches the actual publish date
    #   MySQL indexes on publish + slug keep this query fast

    return render(request, 'blog/post_detail.html', {'post': post})
```

Link to posts in templates using the canonical URL:

```html
<!-- blog/templates/blog/post_list.html -->
{% for post in posts %}
    <article>
        <h2>
            <a href="{{ post.get_absolute_url }}">{{ post.title }}</a>
            {# Resolves to /blog/2025/6/15/django-slugs/ #}
        </h2>
        <p class="date">Published {{ post.publish|date:"F j, Y" }}</p>
    </article>
{% empty %}
    <p>No posts yet.</p>
{% endfor %}
```

### Custom Template Tags and Filters

> 💡 **Analogy:** Django's built-in template tags are like the **standard tools in a Swiss Army knife** — `{% for %}`, `{% if %}`, `{% url %}` handle most jobs. Custom template tags and filters are like **adding a bottle opener or a corkscrew** — purpose-built extensions you snap in when the stock set does not cover your use case.

1️⃣ **WHY** — Templates should stay logic-light, but some presentation needs — "show the five latest posts in every page's sidebar" or "render Markdown to HTML" — cannot be expressed with built-in tags alone. Custom tags and filters let you encapsulate that logic in reusable, testable Python and call it from any template.

2️⃣ **WHEN** — When you need to inject data that does not come from the view (e.g., sidebar widgets), transform output (e.g., Markdown → HTML), or create reusable template fragments across multiple templates.

3️⃣ **HOW**

**File structure** — Django discovers custom tags inside a `templatetags/` package:

```
blog/
├── templatetags/
│   ├── __init__.py          ← required empty file (makes it a Python package)
│   └── blog_tags.py         ← your custom tags and filters
├── models.py
├── views.py
└── ...
```

After creating the `templatetags/` directory, **restart the dev server** so Django registers the new package.

**1 — Simple template tags** (`@register.simple_tag`)

A simple tag runs a Python function and inserts its return value into the template:

```python
# blog/templatetags/blog_tags.py
from django import template
from ..models import Post

register = template.Library()
#   register → an instance of Library that collects your tags and filters

@register.simple_tag
def total_posts():
    """Return the number of published posts."""
    return Post.objects.filter(status='published').count()
    #   The return value is inserted directly into the template output
```

Usage in a template:

```html
{% load blog_tags %}
{# load blog_tags → imports tags/filters from blog/templatetags/blog_tags.py #}

<p>We have {% total_posts %} published posts so far.</p>
{# Output: "We have 42 published posts so far." #}
```

**2 — Inclusion template tags** (`@register.inclusion_tag`)

An inclusion tag renders a **separate template fragment** with its own context — perfect for reusable widgets like sidebars:

```python
# blog/templatetags/blog_tags.py
@register.inclusion_tag('blog/latest_posts.html')
#   Tells Django to render this template with the returned context
def show_latest_posts(count=5):
    """Return the *count* most recent published posts."""
    latest_posts = Post.objects.filter(status='published') \
                               .order_by('-publish')[:count]
    #   Slice limits the queryset — MySQL adds LIMIT to the query

    return {'latest_posts': latest_posts}
    #   The dict becomes the context for latest_posts.html
```

The fragment template:

```html
<!-- blog/templates/blog/latest_posts.html -->
<ul>
{% for post in latest_posts %}
    <li>
        <a href="{{ post.get_absolute_url }}">{{ post.title }}</a>
    </li>
{% endfor %}
</ul>
```

Usage in any template (e.g., a sidebar in `base.html`):

```html
{% load blog_tags %}

<aside>
    <h3>Latest Posts</h3>
    {% show_latest_posts 3 %}
    {# Renders blog/latest_posts.html with the 3 newest posts #}
</aside>
```

**3 — Assignment tags** (using `as` variable syntax)

Any simple tag can store its result in a template variable instead of outputting it directly — use the `as` keyword:

```html
{% load blog_tags %}

{% total_posts as post_count %}
{# Stores the return value in 'post_count' instead of rendering it #}

{% if post_count > 100 %}
    <p>🎉 Over {{ post_count }} posts and counting!</p>
{% else %}
    <p>{{ post_count }} posts published.</p>
{% endif %}
```

No extra Python code is needed — `@register.simple_tag` supports `as` out of the box.

**4 — Custom template filters** (`@register.filter`)

Filters transform a single value. They are called with the `{{ value|filter_name }}` syntax:

```python
# blog/templatetags/blog_tags.py
import markdown
#   pip install markdown — a third-party Markdown library

from django.utils.safestring import mark_safe
#   mark_safe → tells Django the string is safe HTML (skip auto-escaping)

@register.filter(name='markdown')
#   name='markdown' → the name used in templates: {{ value|markdown }}
#   If omitted, Django uses the function name by default
def markdown_format(text):
    """Convert a Markdown string to HTML."""
    return mark_safe(markdown.markdown(text, extensions=['extra', 'codehilite']))
    #   markdown.markdown() converts Markdown → HTML string
    #   mark_safe() prevents Django from escaping the generated HTML
    #   'extra' → adds tables, fenced code blocks, footnotes
    #   'codehilite' → syntax-highlighted code blocks
```

Usage in a template:

```html
{% load blog_tags %}

<div class="post-body">
    {{ post.body|markdown }}
    {# Converts the raw Markdown text in post.body to rendered HTML #}
</div>
```

**5 — Putting it all together** — the complete `blog_tags.py` file:

```python
# blog/templatetags/blog_tags.py
from django import template
from django.utils.safestring import mark_safe
import markdown

from ..models import Post

register = template.Library()
#   One Library instance per module — collects all tags and filters


# ── Simple tag ──────────────────────────────────────────────
@register.simple_tag
def total_posts():
    return Post.objects.filter(status='published').count()
    #   Returns a plain value inserted into the template


# ── Inclusion tag ───────────────────────────────────────────
@register.inclusion_tag('blog/latest_posts.html')
def show_latest_posts(count=5):
    latest_posts = Post.objects.filter(status='published') \
                               .order_by('-publish')[:count]
    return {'latest_posts': latest_posts}
    #   Returns a context dict rendered with latest_posts.html


# ── Custom filter ───────────────────────────────────────────
@register.filter(name='markdown')
def markdown_format(text):
    return mark_safe(markdown.markdown(text, extensions=['extra', 'codehilite']))
    #   Converts Markdown to safe HTML for template output
```

### Class-Based View Mixins

> 💡 **Analogy:** Mixins are like **power-tool attachments**. A drill (your view) does one job well, but snap on a depth stop (LoginRequiredMixin), a right-angle adapter (JsonRequestResponseMixin), or a dust collector (CsrfExemptMixin) and the same drill gains new capabilities — without being replaced.

1️⃣ **WHY** — Mixins add reusable behaviour to class-based views without duplicating code. Need authentication? Add `LoginRequiredMixin`. Need JSON responses? Add `JsonRequestResponseMixin`. Each mixin does one thing, and you compose them freely.

2️⃣ **WHEN** — Whenever you need cross-cutting behaviour (authentication, permissions, JSON handling, logging) shared across multiple views. Prefer mixins over decorating every view individually.

3️⃣ **HOW**

**Built-in Django mixins — restricting access:**

```python
# blog/views.py
from django.contrib.auth.mixins import (
    LoginRequiredMixin,
    PermissionRequiredMixin,
    UserPassesTestMixin,
)
from django.views.generic import CreateView, UpdateView, DeleteView, ListView
from django.urls import reverse_lazy
from .models import Post
from .forms import PostForm


class PostCreateView(LoginRequiredMixin, CreateView):
    #   LoginRequiredMixin → redirects anonymous users to the login page
    #   MUST be the leftmost parent (before CreateView) so its logic runs first
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'

    login_url = '/accounts/login/'
    #   Where to redirect unauthenticated users (default: settings.LOGIN_URL)


class PostUpdateView(PermissionRequiredMixin, UpdateView):
    #   PermissionRequiredMixin → checks that the user has a specific permission
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'

    permission_required = 'blog.change_post'
    #   Django auto-creates 'app_label.action_model' permissions
    #   Raises 403 Forbidden if the user lacks this permission


class PostDeleteView(UserPassesTestMixin, DeleteView):
    #   UserPassesTestMixin → runs a custom test function you define
    model = Post
    template_name = 'blog/post_confirm_delete.html'
    success_url = reverse_lazy('blog:post_list')

    def test_func(self):
        post = self.get_object()
        return self.request.user == post.author
        #   Only the post's author can delete it
        #   Return True → access granted, False → 403 Forbidden
```

**Mixin ordering matters** — Python's MRO (Method Resolution Order) means the leftmost class takes priority:

```python
#   CORRECT — LoginRequiredMixin checks auth BEFORE CreateView runs
class PostCreateView(LoginRequiredMixin, CreateView):
    ...

#   WRONG — CreateView.dispatch() runs first, skipping the auth check
class PostCreateView(CreateView, LoginRequiredMixin):
    ...

#   Rule of thumb: mixins go on the LEFT, the main view goes on the RIGHT
```

**Creating a custom mixin:**

```python
# blog/mixins.py
from django.contrib import messages

class AuthorRequiredMixin:
    """Verify that the current user is the object's author."""

    def dispatch(self, request, *args, **kwargs):
        #   dispatch() is called before get() or post()
        #   Overriding it lets us intercept every request method

        obj = self.get_object()
        if obj.author != request.user:
            messages.error(request, 'You are not the author of this post.')
            return self.handle_no_permission()
            #   handle_no_permission() raises 403 by default

        return super().dispatch(request, *args, **kwargs)
        #   super() → passes control to the next class in the MRO chain
```

Using the custom mixin:

```python
# blog/views.py
from .mixins import AuthorRequiredMixin

class PostUpdateView(LoginRequiredMixin, AuthorRequiredMixin, UpdateView):
    #   First checks login, then checks authorship, then runs the update
    model = Post
    form_class = PostForm
    template_name = 'blog/post_form.html'
```

**Third-party mixins with django-braces:**

Install:

```bash
pip install django-braces
#   Provides dozens of ready-made mixins for common view patterns
```

```python
# blog/views.py
from braces.views import (
    JsonRequestResponseMixin,
    CsrfExemptMixin,
    SelectRelatedMixin,
    StaffuserRequiredMixin,
)
from django.views.generic import ListView, View
from .models import Post


class PostApiView(CsrfExemptMixin, JsonRequestResponseMixin, View):
    #   CsrfExemptMixin → disables CSRF checks (use only for API endpoints)
    #   JsonRequestResponseMixin → parses JSON body, provides render_json_response()

    def post(self, request, *args, **kwargs):
        data = self.request_json
        #   request_json → the parsed JSON body from the request

        title = data.get('title', '')
        return self.render_json_response({'received': title, 'status': 'ok'})
        #   render_json_response() → returns a JsonResponse


class DashboardView(StaffuserRequiredMixin, ListView):
    #   StaffuserRequiredMixin → allows only users with is_staff=True
    model = Post
    template_name = 'blog/dashboard.html'
    context_object_name = 'posts'


class PostListView(SelectRelatedMixin, ListView):
    #   SelectRelatedMixin → automatically adds select_related() to the queryset
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'

    select_related = ['author']
    #   Joins the author table in a single query — avoids N+1 on MySQL
```

Common django-braces mixins at a glance:

| Mixin | Purpose |
|---|---|
| `LoginRequiredMixin` | Redirect anonymous users (also built-in since Django 1.9) |
| `StaffuserRequiredMixin` | Restrict to `is_staff=True` users |
| `SuperuserRequiredMixin` | Restrict to `is_superuser=True` users |
| `CsrfExemptMixin` | Skip CSRF verification on a view |
| `JsonRequestResponseMixin` | Parse JSON request bodies and return JSON responses |
| `SelectRelatedMixin` | Auto `select_related()` on the queryset |
| `PrefetchRelatedMixin` | Auto `prefetch_related()` on the queryset |
| `FormValidMessageMixin` | Show a success message after valid form submission |

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


### Formsets

> 💡 **Analogy:** A formset is like a **stack of identical paper forms** clipped together — each form captures one item (e.g., one course module), and the clip (the management form) tells Django how many forms are in the stack, which ones are new, and which ones should be thrown away.

1️⃣ **WHY** — When you need users to submit multiple instances of the same form at once (e.g., adding several course modules, bulk-editing rows), handling each form individually is tedious. Formsets manage a collection of identical forms as a single unit, with built-in tracking of additions, changes, and deletions.

2️⃣ **WHEN** — Bulk creation or editing of related objects: course modules for a course, order line-items for an order, phone numbers for a contact, or any parent → children relationship where children are edited inline.

3️⃣ **HOW**

**Plain formset with `formset_factory`**

```python
# courses/forms.py
from django import forms
from django.forms import formset_factory

class ModuleBaseForm(forms.Form):
    title = forms.CharField(max_length=200)
    description = forms.CharField(
        widget=forms.Textarea(attrs={'rows': 3}),
        required=False,
    )
    #   required=False → description is optional for each module

ModuleFormSet = formset_factory(
    ModuleBaseForm,
    extra=3,
    #   extra → number of empty forms shown by default
    max_num=20,
    #   max_num → hard upper limit on total forms accepted
    min_num=1,
    #   min_num → at least one form must be submitted
    validate_min=True,
    #   validate_min → actually enforce min_num during validation
)
```

Using the plain formset in a view:

```python
# courses/views.py
from django.shortcuts import render, redirect
from .forms import ModuleFormSet

def add_modules(request):
    if request.method == 'POST':
        formset = ModuleFormSet(request.POST)
        #   Bind POST data to the formset (just like a single form)

        if formset.is_valid():
            for form in formset:
                if form.cleaned_data and not form.cleaned_data.get('DELETE', False):
                    #   Skip empty forms and forms marked for deletion
                    title = form.cleaned_data['title']
                    description = form.cleaned_data['description']
                    # ... save each module to the database ...
            return redirect('courses:module_list')
    else:
        formset = ModuleFormSet()
        #   Unbound formset — renders 'extra' empty forms

    return render(request, 'courses/add_modules.html', {'formset': formset})
```

**Model-backed formset with `modelformset_factory`**

```python
# courses/forms.py
from django.forms import modelformset_factory
from .models import Module

ModuleModelFormSet = modelformset_factory(
    Module,
    #   Model to create/edit instances of
    fields=['title', 'description', 'order'],
    #   Explicit field list — same security practice as ModelForm
    extra=2,
    #   Show 2 blank forms for adding new modules
    can_delete=True,
    #   can_delete → adds a DELETE checkbox to each form
)
```

```python
# courses/views.py
from .forms import ModuleModelFormSet

def manage_all_modules(request):
    if request.method == 'POST':
        formset = ModuleModelFormSet(request.POST)
        if formset.is_valid():
            formset.save()
            #   .save() → creates new, updates changed, deletes checked instances
            return redirect('courses:module_list')
    else:
        formset = ModuleModelFormSet()
        #   Unbound → loads existing Module rows from the database
    return render(request, 'courses/manage_modules.html', {'formset': formset})
```

**Inline formset with `inlineformset_factory` — course modules for a specific course**

```python
# courses/forms.py
from django.forms import inlineformset_factory
from .models import Course, Module

ModuleInlineFormSet = inlineformset_factory(
    Course,
    #   Parent model
    Module,
    #   Child model (must have a ForeignKey to Course)
    fields=['title', 'description', 'order'],
    extra=2,
    can_delete=True,
    #   Allows removing existing modules via a checkbox
    can_order=True,
    #   can_order → adds an ORDER field for manual sorting
)
```

```python
# courses/views.py
from django.shortcuts import get_object_or_404
from .models import Course
from .forms import ModuleInlineFormSet

def manage_course_modules(request, course_id):
    course = get_object_or_404(Course, pk=course_id)
    #   The parent instance whose children we are editing

    if request.method == 'POST':
        formset = ModuleInlineFormSet(
            request.POST,
            instance=course,
            #   instance → ties every child form to this specific course
        )
        if formset.is_valid():
            formset.save()
            #   Creates / updates / deletes Module rows linked to this course
            return redirect('courses:course_detail', pk=course.pk)
    else:
        formset = ModuleInlineFormSet(instance=course)
        #   Pre-populates forms with existing modules for this course

    return render(request, 'courses/manage_modules.html', {
        'course': course,
        'formset': formset,
    })
```

Rendering formsets in a template (including the **management form**):

```html
<!-- courses/templates/courses/manage_modules.html -->
<h2>Modules for "{{ course.title }}"</h2>

<form method="post">
    {% csrf_token %}

    {{ formset.management_form }}
    {# management_form → hidden fields that track total, initial, min, and max #}
    {# form counts.  REQUIRED — omitting it causes a ManagementForm error.    #}

    <table>
        <thead>
            <tr>
                <th>Title</th>
                <th>Description</th>
                <th>Order</th>
                <th>Delete?</th>
            </tr>
        </thead>
        <tbody>
            {% for form in formset %}
            <tr>
                {{ form.id }}
                {# form.id → hidden input with the object PK; needed for updates #}

                <td>{{ form.title }}</td>
                <td>{{ form.description }}</td>
                <td>{{ form.order }}</td>
                <td>{{ form.DELETE }}</td>
                {# DELETE → checkbox rendered by can_delete=True #}

                {% if form.errors %}
                <tr>
                    <td colspan="4">
                        {{ form.errors }}
                        {# Per-form errors displayed below the row #}
                    </td>
                </tr>
                {% endif %}
            </tr>
            {% endfor %}
        </tbody>
    </table>

    {% if formset.non_form_errors %}
        <div class="errors">{{ formset.non_form_errors }}</div>
        {# non_form_errors → formset-wide validation errors (e.g., min_num) #}
    {% endif %}

    <button type="submit">Save Modules</button>
</form>
```

Adding forms dynamically with JavaScript (the **empty_form** trick):

```html
{# Hidden template row used by JavaScript to add new forms #}
<div id="empty-form" style="display:none;">
    {{ formset.empty_form }}
    {# empty_form → a single form with __prefix__ as its index placeholder #}
</div>

<button type="button" id="add-form">+ Add Module</button>

<script>
document.getElementById('add-form').addEventListener('click', function () {
    const totalForms = document.getElementById('id_form-TOTAL_FORMS');
    //   TOTAL_FORMS → management-form field tracking the current form count
    const currentCount = parseInt(totalForms.value);

    const template = document.getElementById('empty-form').innerHTML;
    const newForm = template.replace(/__prefix__/g, currentCount);
    //   Replace __prefix__ with the next form index (0-based)

    document.querySelector('tbody').insertAdjacentHTML('beforeend', newForm);
    totalForms.value = currentCount + 1;
    //   Increment TOTAL_FORMS so Django processes the new form
});
</script>
```

### Cleaning Form Fields

> 💡 **Analogy:** Cleaning a form field is like a **mail room sorting letters**. Each letter (field value) first goes through its own slot for basic inspection (`clean_<fieldname>`). Then a supervisor reviews the whole batch together (`clean()`) to catch problems that only appear when comparing multiple letters — like two letters with conflicting addresses.

1️⃣ **WHY** — Built-in validators catch common issues (required, max_length, valid email), but real applications need custom rules: normalizing URLs, stripping whitespace, rejecting banned words, or enforcing cross-field constraints like "end date must be after start date." The `clean_<fieldname>()` and `clean()` hooks let you add these rules in a structured, reusable way.

2️⃣ **WHEN** — Whenever built-in field validation is not enough: sanitizing URLs for a bookmarking app, ensuring a username is lowercase, validating that a discount percentage makes sense relative to the price, or checking that two password fields match.

3️⃣ **HOW**

**Single-field cleaning with `clean_<fieldname>()`**

```python
# images/forms.py
from django import forms
from urllib.parse import urlparse

class ImageBookmarkForm(forms.Form):
    title = forms.CharField(max_length=200)
    url = forms.URLField()
    #   URLField → basic URL format validation built-in
    description = forms.CharField(
        widget=forms.Textarea(attrs={'rows': 3}),
        required=False,
    )

    def clean_title(self):
        """Strip whitespace and enforce minimum length."""
        title = self.cleaned_data['title'].strip()
        #   .strip() → remove leading/trailing whitespace
        if len(title) < 3:
            raise forms.ValidationError(
                'Title must be at least 3 characters after trimming whitespace.'
            )
        return title
        #   Always return the cleaned value — Django stores it back in cleaned_data

    def clean_url(self):
        """Validate and normalize the image URL."""
        url = self.cleaned_data['url']
        parsed = urlparse(url)
        #   urlparse → splits URL into scheme, netloc, path, etc.

        valid_extensions = ('.jpg', '.jpeg', '.png', '.gif', '.webp')
        path_lower = parsed.path.lower()

        if not path_lower.endswith(valid_extensions):
            raise forms.ValidationError(
                'The URL must point to an image file '
                '(jpg, jpeg, png, gif, or webp).'
            )
            #   ValidationError → attaches this message to the 'url' field

        if parsed.scheme not in ('http', 'https'):
            raise forms.ValidationError(
                'Only HTTP and HTTPS URLs are allowed.'
            )

        # Normalize: force HTTPS
        if parsed.scheme == 'http':
            url = url.replace('http://', 'https://', 1)
            #   Upgrade to HTTPS for security

        return url
```

**Cross-field validation with `clean()`**

```python
# events/forms.py
from django import forms
from datetime import date

class EventForm(forms.Form):
    name = forms.CharField(max_length=200)
    start_date = forms.DateField(widget=forms.DateInput(attrs={'type': 'date'}))
    end_date = forms.DateField(widget=forms.DateInput(attrs={'type': 'date'}))
    max_attendees = forms.IntegerField(min_value=1)
    current_attendees = forms.IntegerField(min_value=0)

    def clean_name(self):
        """Normalize event name to title case."""
        name = self.cleaned_data['name'].strip()
        return name.title()
        #   .title() → "django meetup" becomes "Django Meetup"

    def clean(self):
        """Cross-field validation — compare multiple fields together."""
        cleaned_data = super().clean()
        #   super().clean() → runs the parent clean and returns cleaned_data
        #   Always call super() first to ensure individual fields are validated

        start = cleaned_data.get('start_date')
        end = cleaned_data.get('end_date')

        if start and end and end < start:
            raise forms.ValidationError(
                'End date must be on or after the start date.'
            )
            #   Error raised here is non-field: appears in form.non_field_errors

        if start and start < date.today():
            self.add_error('start_date', 'Start date cannot be in the past.')
            #   add_error → attaches the error to a specific field
            #   Preferred over raise when you want to report multiple errors

        max_att = cleaned_data.get('max_attendees')
        cur_att = cleaned_data.get('current_attendees')
        if max_att and cur_att and cur_att > max_att:
            self.add_error(
                'current_attendees',
                'Current attendees cannot exceed maximum capacity.'
            )

        return cleaned_data
        #   Always return cleaned_data from clean()
```

Using cleaned fields in a ModelForm (image bookmarking example):

```python
# images/forms.py
from django.forms import ModelForm
from .models import Image
from urllib.parse import urlparse

class ImageModelForm(ModelForm):
    class Meta:
        model = Image
        fields = ['title', 'url', 'description']

    def clean_url(self):
        """Ensure URL points to an image and strip query parameters."""
        url = self.cleaned_data['url']
        parsed = urlparse(url)
        valid_extensions = ('.jpg', '.jpeg', '.png', '.gif', '.webp')

        if not parsed.path.lower().endswith(valid_extensions):
            raise forms.ValidationError(
                'URL does not point to a valid image format.'
            )

        # Strip query string and fragment for a clean canonical URL
        clean_url = f'{parsed.scheme}://{parsed.netloc}{parsed.path}'
        #   Rebuild URL without ?query or #fragment

        if Image.objects.filter(url=clean_url).exclude(pk=self.instance.pk).exists():
            raise forms.ValidationError(
                'An image with this URL has already been bookmarked.'
            )
            #   Uniqueness check — prevent duplicate bookmarks

        return clean_url

    def clean_description(self):
        """Strip whitespace and cap length for database storage."""
        desc = self.cleaned_data.get('description', '')
        desc = desc.strip()
        #   Remove accidental leading/trailing whitespace

        if len(desc) > 2000:
            raise forms.ValidationError(
                'Description must be 2000 characters or fewer.'
            )
        return desc
```

Displaying field-level and non-field errors in a template:

```html
<!-- images/templates/images/bookmark_form.html -->
<form method="post">
    {% csrf_token %}

    {% if form.non_field_errors %}
        <div class="alert alert-danger">
            {% for error in form.non_field_errors %}
                <p>{{ error }}</p>
            {% endfor %}
        </div>
        {# non_field_errors → errors raised in clean() without add_error #}
    {% endif %}

    {% for field in form %}
        <div class="mb-3">
            {{ field.label_tag }}
            {{ field }}
            {% for error in field.errors %}
                <span class="text-danger">{{ error }}</span>
                {# field.errors → errors from clean_<fieldname> or add_error #}
            {% endfor %}
        </div>
    {% endfor %}

    <button type="submit">Save Bookmark</button>
</form>
```

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


### Built-in Authentication Views

> 💡 **Analogy:** Django's built-in auth views are like **pre-built doors with locks** in your apartment building — login, logout, change password, and reset password doors are already manufactured and tested. You just choose the style (template) and where to place them (URL configuration), instead of building each door mechanism from scratch.

1️⃣ **WHY** — Authentication workflows (login, logout, password change, password reset) follow well-known patterns that are easy to get wrong from a security perspective. Django provides eight battle-tested class-based views that handle form display, credential validation, token generation, and email dispatch — all with secure defaults.

2️⃣ **WHEN** — Use these views in any project that requires user authentication. They cover the full lifecycle: `LoginView`, `LogoutView`, `PasswordChangeView`, `PasswordChangeDoneView`, `PasswordResetView`, `PasswordResetDoneView`, `PasswordResetConfirmView`, and `PasswordResetCompleteView`.

3️⃣ **HOW**

Include all authentication URLs at once:

```python
# mysite/urls.py
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('admin/', admin.site.urls),

    # --- Login and Logout ---
    path('account/login/', auth_views.LoginView.as_view(), name='login'),
    #   Renders a login form and authenticates the user on POST
    #   Looks for a template at registration/login.html by default

    path('account/logout/', auth_views.LogoutView.as_view(), name='logout'),
    #   Logs the user out and redirects to LOGOUT_REDIRECT_URL

    # --- Password Change (logged-in users) ---
    path(
        'account/password-change/',
        auth_views.PasswordChangeView.as_view(),
        name='password_change',
    ),
    #   Shows a form asking for old password + new password (twice)
    #   Looks for registration/password_change_form.html by default

    path(
        'account/password-change/done/',
        auth_views.PasswordChangeDoneView.as_view(),
        name='password_change_done',
    ),
    #   Confirmation page shown after a successful password change

    # --- Password Reset (forgotten password, logged-out users) ---
    path(
        'account/password-reset/',
        auth_views.PasswordResetView.as_view(),
        name='password_reset',
    ),
    #   Asks for the user's email and sends a reset link
    #   Looks for registration/password_reset_form.html

    path(
        'account/password-reset/done/',
        auth_views.PasswordResetDoneView.as_view(),
        name='password_reset_done',
    ),
    #   Tells the user to check their email

    path(
        'account/password-reset/<uidb64>/<token>/',
        auth_views.PasswordResetConfirmView.as_view(),
        name='password_reset_confirm',
    ),
    #   Validates the token and lets the user set a new password
    #   <uidb64> is the user ID encoded in base64
    #   <token> is a one-time-use token generated by Django

    path(
        'account/password-reset/complete/',
        auth_views.PasswordResetCompleteView.as_view(),
        name='password_reset_complete',
    ),
    #   Final confirmation that the password has been reset

    path('blog/', include('blog.urls')),
]
```

Configure redirect targets and email backend in settings:

```python
# settings.py
LOGIN_REDIRECT_URL = 'dashboard'
#   Where to redirect after a successful login (URL name or path)

LOGOUT_REDIRECT_URL = 'login'
#   Where to redirect after logout

LOGIN_URL = 'login'
#   Where @login_required sends unauthenticated users

EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
#   Prints password-reset emails to the console during development
#   Replace with an SMTP backend in production
```

Create the login template:

```html
<!-- templates/registration/login.html -->
{% extends "base.html" %}

{% block title %}Log In{% endblock %}

{% block content %}
<h2>Log In</h2>

{% if form.errors %}
    <p class="error">Your username and password didn't match. Please try again.</p>
    <!--  Django populates form.errors automatically on failed login  -->
{% endif %}

<form method="post">
    {% csrf_token %}
    <!--  CSRF token is required for every POST form  -->

    {{ form.as_p }}
    <!--  Renders username and password fields wrapped in <p> tags  -->

    <input type="hidden" name="next" value="{{ next }}" />
    <!--  After login, redirect to the page the user originally requested  -->

    <button type="submit">Log In</button>
</form>

<p>
    <a href="{% url 'password_reset' %}">Forgot your password?</a>
</p>
{% endblock %}
```

Create the password change template:

```html
<!-- templates/registration/password_change_form.html -->
{% extends "base.html" %}

{% block title %}Change Your Password{% endblock %}

{% block content %}
<h2>Change Your Password</h2>
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <!--  Renders old_password, new_password1, and new_password2 fields  -->
    <button type="submit">Change Password</button>
</form>
{% endblock %}
```

```html
<!-- templates/registration/password_change_done.html -->
{% extends "base.html" %}

{% block title %}Password Changed{% endblock %}

{% block content %}
<h2>Password Changed</h2>
<p>Your password has been changed successfully.</p>
{% endblock %}
```

Create the password reset templates:

```html
<!-- templates/registration/password_reset_form.html -->
{% extends "base.html" %}

{% block title %}Reset Your Password{% endblock %}

{% block content %}
<h2>Reset Your Password</h2>
<p>Enter your email address to receive a password reset link.</p>
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <!--  Renders a single email field  -->
    <button type="submit">Send Reset Link</button>
</form>
{% endblock %}
```

```html
<!-- templates/registration/password_reset_done.html -->
{% extends "base.html" %}

{% block title %}Password Reset Sent{% endblock %}

{% block content %}
<h2>Check Your Email</h2>
<p>We've sent you an email with a link to reset your password.</p>
<p>If you don't receive it, make sure you entered the address you registered with.</p>
{% endblock %}
```

```html
<!-- templates/registration/password_reset_confirm.html -->
{% extends "base.html" %}

{% block title %}Set New Password{% endblock %}

{% block content %}
<h2>Set New Password</h2>
{% if validlink %}
    <form method="post">
        {% csrf_token %}
        {{ form.as_p }}
        <!--  Renders new_password1 and new_password2 fields  -->
        <button type="submit">Set Password</button>
    </form>
{% else %}
    <p>This password reset link is invalid or has expired.
       Please <a href="{% url 'password_reset' %}">request a new one</a>.</p>
    <!--  validlink is False when the token has been used or is expired  -->
{% endif %}
{% endblock %}
```

```html
<!-- templates/registration/password_reset_complete.html -->
{% extends "base.html" %}

{% block title %}Password Reset Complete{% endblock %}

{% block content %}
<h2>Password Reset Complete</h2>
<p>Your password has been set. You can now
   <a href="{% url 'login' %}">log in</a> with your new password.</p>
{% endblock %}
```

Customize a built-in view by overriding attributes:

```python
# mysite/urls.py — customizing LoginView
path(
    'account/login/',
    auth_views.LoginView.as_view(
        template_name='account/login.html',
        #   Use a custom template instead of registration/login.html

        redirect_authenticated_user=True,
        #   If a logged-in user visits /login/, redirect them immediately
    ),
    name='login',
),
```

Password reset email template (optional customization):

```html
<!-- templates/registration/password_reset_email.html -->
Someone requested a password reset for your account at {{ site_name }}.

Click the link below to set a new password:
{{ protocol }}://{{ domain }}{% url 'password_reset_confirm' uidb64=uid token=token %}

If you did not request this, ignore this email.
<!--  Django passes uid, token, protocol, domain, and site_name to this template  -->
```

### User Profiles and Extending the User Model

> 💡 **Analogy:** Django's built-in `User` model is like a **government-issued ID card** — it has the essentials (name, email, password) but no room for your photo, bio, or date of birth. A `Profile` model is like a **personal portfolio** attached to that ID card with a paper clip (a one-to-one relationship), letting you store additional information without modifying the original card.

1️⃣ **WHY** — The built-in `User` model covers authentication fields (username, email, password, first/last name) but real applications need more — profile pictures, bios, dates of birth, social links, and preferences. Rather than modifying the `User` model directly (which complicates upgrades), Django recommends creating a separate `Profile` model linked via a `OneToOneField`.

2️⃣ **WHEN** — Whenever your application needs to store user-specific data beyond what `django.contrib.auth.models.User` provides. This pattern is the standard approach for most Django projects.

3️⃣ **HOW**

Install Pillow for `ImageField` support:

```bash
pip install Pillow
#   Pillow is required for ImageField — it handles image processing
#   Without it, Django raises an error when you use ImageField
```

Define the Profile model:

```python
# account/models.py
from django.db import models
from django.conf import settings


class Profile(models.Model):
    user = models.OneToOneField(
        settings.AUTH_USER_MODEL,
        on_delete=models.CASCADE,
    )
    #   Links each Profile to exactly one User
    #   settings.AUTH_USER_MODEL is preferred over importing User directly
    #   on_delete=CASCADE deletes the profile when the user is deleted

    date_of_birth = models.DateField(blank=True, null=True)
    #   Optional date of birth — blank=True allows empty forms,
    #   null=True allows NULL in the database

    bio = models.TextField(blank=True)
    #   A free-text biography — blank=True means it's not required

    photo = models.ImageField(
        upload_to='users/%Y/%m/%d/',
        blank=True,
    )
    #   Profile photo uploaded to MEDIA_ROOT/users/YYYY/MM/DD/
    #   ImageField requires Pillow to be installed

    def __str__(self):
        return f'Profile of {self.user.username}'
```

Configure media file settings:

```python
# settings.py
import os

MEDIA_URL = '/media/'
#   URL prefix for serving uploaded files

MEDIA_ROOT = os.path.join(BASE_DIR, 'media/')
#   Absolute filesystem path where uploaded files are stored
```

Serve media files during development:

```python
# mysite/urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    path('admin/', admin.site.urls),
    path('account/', include('account.urls')),
]

if settings.DEBUG:
    urlpatterns += static(
        settings.MEDIA_URL,
        document_root=settings.MEDIA_ROOT,
    )
    #   In development, Django serves uploaded files directly
    #   In production, your web server (Nginx) handles this
```

Create and apply migrations:

```bash
python manage.py makemigrations account
#   Generates a migration file for the new Profile model

python manage.py migrate
#   Applies the migration — creates the account_profile table in MySQL
```

Auto-create a Profile whenever a new User is created using signals:

```python
# account/signals.py
from django.db.models.signals import post_save
from django.dispatch import receiver
from django.conf import settings
from .models import Profile


@receiver(post_save, sender=settings.AUTH_USER_MODEL)
def create_user_profile(sender, instance, created, **kwargs):
    #   sender = the User model class
    #   instance = the actual User object that was saved
    #   created = True if this is a brand-new user, False if updating
    if created:
        Profile.objects.create(user=instance)
        #   Automatically create a Profile for every new User
```

Register the signal in the app config:

```python
# account/apps.py
from django.apps import AppConfig


class AccountConfig(AppConfig):
    default_auto_field = 'django.db.models.BigAutoField'
    name = 'account'

    def ready(self):
        import account.signals
        #   Import signals module so the @receiver decorators are registered
        #   ready() is called once when Django starts up
```

Create forms for editing the User and Profile together:

```python
# account/forms.py
from django import forms
from django.contrib.auth.models import User
from .models import Profile


class UserEditForm(forms.ModelForm):
    class Meta:
        model = User
        fields = ['first_name', 'last_name', 'email']
        #   Allow users to edit their basic info
        #   Do NOT include username or password here


class ProfileEditForm(forms.ModelForm):
    class Meta:
        model = Profile
        fields = ['date_of_birth', 'bio', 'photo']
        #   Allow users to edit their extended profile data
```

Build a view that handles both forms simultaneously:

```python
# account/views.py
from django.contrib.auth.decorators import login_required
from django.shortcuts import render
from django.contrib import messages
from .forms import UserEditForm, ProfileEditForm


@login_required
def edit_profile(request):
    if request.method == 'POST':
        user_form = UserEditForm(
            instance=request.user,
            data=request.POST,
        )
        #   Bind the form to the current user's data

        profile_form = ProfileEditForm(
            instance=request.user.profile,
            data=request.POST,
            files=request.FILES,
        )
        #   Bind the form to the current user's profile
        #   files=request.FILES is required for the photo ImageField

        if user_form.is_valid() and profile_form.is_valid():
            user_form.save()
            profile_form.save()
            #   Save both forms — updates User and Profile in the database
            messages.success(request, 'Profile updated successfully.')
        else:
            messages.error(request, 'Error updating your profile.')
    else:
        user_form = UserEditForm(instance=request.user)
        profile_form = ProfileEditForm(instance=request.user.profile)

    return render(
        request,
        'account/edit_profile.html',
        {
            'user_form': user_form,
            'profile_form': profile_form,
        },
    )
```

Create the edit profile template:

```html
<!-- templates/account/edit_profile.html -->
{% extends "base.html" %}

{% block title %}Edit Profile{% endblock %}

{% block content %}
<h2>Edit Your Profile</h2>

<form method="post" enctype="multipart/form-data">
    <!--  enctype="multipart/form-data" is required for file uploads  -->
    {% csrf_token %}

    {{ user_form.as_p }}
    <!--  Renders first_name, last_name, email fields  -->

    {{ profile_form.as_p }}
    <!--  Renders date_of_birth, bio, photo fields  -->

    <button type="submit">Save Changes</button>
</form>
{% endblock %}
```

Display the profile photo in a template:

```html
<!-- templates/account/dashboard.html -->
{% extends "base.html" %}

{% block content %}
<h2>Dashboard</h2>
<p>Welcome, {{ request.user.first_name }}!</p>

{% if request.user.profile.photo %}
    <img src="{{ request.user.profile.photo.url }}"
         alt="Profile photo"
         width="150" />
    <!--  .url returns the full URL path to the uploaded image  -->
{% endif %}

<p>{{ request.user.profile.bio }}</p>
<a href="{% url 'edit_profile' %}">Edit profile</a>
{% endblock %}
```

Register the Profile model in the admin:

```python
# account/admin.py
from django.contrib import admin
from .models import Profile


@admin.register(Profile)
class ProfileAdmin(admin.ModelAdmin):
    list_display = ['user', 'date_of_birth', 'photo']
    #   Show these columns in the admin list view
    raw_id_fields = ['user']
    #   Use a lookup widget instead of a dropdown for the user field
    #   Much faster when you have thousands of users
```

### Custom Authentication Backends

> 💡 **Analogy:** Django's authentication backend is like the **lock mechanism** on your front door. The default lock (username + password) works fine, but you can swap it for a fingerprint scanner (email login), a key card (token auth), or even have multiple locks that any one of them can open. Django tries each backend in order until one succeeds.

1️⃣ **WHY** — By default, Django authenticates users with their username and password using `ModelBackend`. But many applications need alternative authentication methods — logging in with an email address, authenticating against an LDAP directory, or checking credentials from an external API. Custom backends let you plug in any authentication logic without modifying Django's core.

2️⃣ **WHEN** — Use a custom backend when you need to authenticate users by something other than their username (most commonly email), or when credentials are verified by an external system. You can stack multiple backends so that Django tries each one in order.

3️⃣ **HOW**

Create a custom backend that allows login with email:

```python
# account/authentication.py
from django.contrib.auth.backends import BaseBackend
from django.contrib.auth.models import User


class EmailAuthBackend(BaseBackend):
    """
    Authenticate using an email address instead of a username.
    """

    def authenticate(self, request, username=None, password=None):
        #   Django calls authenticate() on each backend in order
        #   username parameter receives whatever the user typed in the
        #   username field — in our case, it will be an email address
        try:
            user = User.objects.get(email=username)
            #   Look up the user by email instead of username
        except (User.DoesNotExist, User.MultipleObjectsReturned):
            #   User.DoesNotExist — no user with that email
            #   User.MultipleObjectsReturned — duplicate emails in the database
            return None

        if user.check_password(password):
            #   check_password() hashes the raw password and compares
            #   it to the stored hash — never compare passwords directly
            return user
        return None
        #   Return None to signal that this backend cannot authenticate
        #   the user — Django will try the next backend in the list

    def get_user(self, user_id):
        #   Django calls get_user() to retrieve the user from the session
        #   This method is required by every authentication backend
        try:
            return User.objects.get(pk=user_id)
        except User.DoesNotExist:
            return None
```

Register the backend in settings:

```python
# settings.py
AUTHENTICATION_BACKENDS = [
    'django.contrib.auth.backends.ModelBackend',
    #   The default backend — authenticates with username + password
    #   Keep this so users can still log in with their username

    'account.authentication.EmailAuthBackend',
    #   Our custom backend — authenticates with email + password
    #   Django tries backends in order: first ModelBackend, then EmailAuthBackend
]
```

How Django processes the backends:

```python
# When you call django.contrib.auth.authenticate():
from django.contrib.auth import authenticate

user = authenticate(request, username='john@example.com', password='secret')
#   Step 1: Django calls ModelBackend.authenticate()
#           → tries to find a user with username='john@example.com'
#           → no match → returns None
#
#   Step 2: Django calls EmailAuthBackend.authenticate()
#           → tries to find a user with email='john@example.com'
#           → match found → checks password → returns the User object
#
#   If ALL backends return None, authenticate() returns None
```

Use the backend in a custom login view:

```python
# account/views.py
from django.contrib.auth import authenticate, login
from django.shortcuts import render, redirect
from django.http import HttpResponse


def user_login(request):
    if request.method == 'POST':
        username = request.POST.get('username')
        password = request.POST.get('password')

        user = authenticate(request, username=username, password=password)
        #   Tries each backend in AUTHENTICATION_BACKENDS in order
        #   Works with both username and email because we have two backends

        if user is not None:
            if user.is_active:
                login(request, user)
                #   login() saves the user ID in the session
                return redirect('dashboard')
            else:
                return HttpResponse('Account is disabled.')
        else:
            return HttpResponse('Invalid credentials.')
    else:
        return render(request, 'account/login.html')
```

### Social Authentication

> 💡 **Analogy:** Social authentication is like using your **driver's license to board a flight** — you already proved your identity to the DMV (Google, Facebook, etc.), so the airline (your Django app) trusts that verification instead of making you fill out new paperwork. OAuth is the standardized protocol that makes this trust handoff work.

1️⃣ **WHY** — Many users prefer signing in with their existing Google, GitHub, or Facebook accounts rather than creating yet another username and password. Social authentication improves user experience, increases sign-up rates, and offloads password security to the identity provider. The `social-auth-app-django` library integrates the OAuth flow into Django seamlessly.

2️⃣ **WHEN** — Use social authentication when you want to offer "Sign in with Google/GitHub/Facebook" buttons. It is especially useful for consumer-facing applications where reducing sign-up friction matters.

3️⃣ **HOW**

Install the social auth library:

```bash
pip install social-auth-app-django
#   Provides Django integration for Python Social Auth
#   Supports Google, GitHub, Facebook, Twitter, and many more providers
```

Add it to your installed apps and configure the backends:

```python
# settings.py
INSTALLED_APPS = [
    # ...
    'social_django',
    #   Adds the social auth models and template context processors
]

AUTHENTICATION_BACKENDS = [
    'social_core.backends.google.GoogleOAuth2',
    #   Enables "Sign in with Google" via OAuth 2.0

    'django.contrib.auth.backends.ModelBackend',
    #   Keep the default backend so username/password login still works

    'account.authentication.EmailAuthBackend',
    #   Our custom email backend (from the previous section)
]
```

Run migrations to create the social auth database tables:

```bash
python manage.py migrate
#   social_django adds tables to store social auth associations,
#   nonces, and user social auth links in your MySQL database
```

Add the social auth URL patterns:

```python
# mysite/urls.py
urlpatterns = [
    path('admin/', admin.site.urls),
    path('account/', include('account.urls')),
    path('social-auth/', include('social_django.urls', namespace='social')),
    #   Adds OAuth callback URLs under /social-auth/
    #   The namespace 'social' lets you reference URLs like {% url 'social:begin' 'google-oauth2' %}
]
```

Set up Google OAuth credentials:

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project (or select an existing one)
3. Navigate to **APIs & Services → Credentials**
4. Click **Create Credentials → OAuth 2.0 Client ID**
5. Set the **Authorized redirect URI** to `https://127.0.0.1:8000/social-auth/complete/google-oauth2/` (HTTPS is required by Google — see the [SSL/TLS Certificates](#ssltls-certificates) section for running the dev server over HTTPS)
6. Copy the **Client ID** and **Client Secret**

```python
# settings.py — Google OAuth configuration
SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = 'your-google-client-id.apps.googleusercontent.com'
#   The Client ID from Google Cloud Console

SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = 'your-google-client-secret'
#   The Client Secret from Google Cloud Console
#   In production, load these from environment variables:
#   SOCIAL_AUTH_GOOGLE_OAUTH2_KEY = os.environ.get('GOOGLE_OAUTH2_KEY')
#   SOCIAL_AUTH_GOOGLE_OAUTH2_SECRET = os.environ.get('GOOGLE_OAUTH2_SECRET')

SOCIAL_AUTH_GOOGLE_OAUTH2_SCOPE = [
    'https://www.googleapis.com/auth/userinfo.email',
    'https://www.googleapis.com/auth/userinfo.profile',
]
#   Request access to the user's email and basic profile information
```

Configure the social auth pipeline and URL settings:

```python
# settings.py
SOCIAL_AUTH_PIPELINE = [
    'social_core.pipeline.social_auth.social_details',
    #   Extracts user details (email, name) from the provider's response

    'social_core.pipeline.social_auth.social_uid',
    #   Gets the unique user ID from the provider

    'social_core.pipeline.social_auth.auth_allowed',
    #   Checks that the provider is in the allowed list

    'social_core.pipeline.social_auth.social_user',
    #   Looks for an existing social auth association in the database

    'social_core.pipeline.user.get_username',
    #   Generates a unique username for new users

    'social_core.pipeline.user.create_user',
    #   Creates a new Django User if one doesn't exist

    'account.pipeline.create_profile',
    #   Custom step — creates a Profile for social auth users (see below)

    'social_core.pipeline.social_auth.associate_user',
    #   Associates the social account with the Django User

    'social_core.pipeline.social_auth.load_extra_data',
    #   Loads any extra data from the provider into the social auth model

    'social_core.pipeline.user.user_details',
    #   Updates the User model with details from the provider
]

SOCIAL_AUTH_URL_NAMESPACE = 'social'
#   Must match the namespace used in urls.py
```

Create a custom pipeline step to build a Profile for social auth users:

```python
# account/pipeline.py
from .models import Profile


def create_profile(backend, user, response, is_new=False, *args, **kwargs):
    #   backend = the social auth backend (e.g., GoogleOAuth2)
    #   user = the Django User object
    #   response = the raw response from the provider
    #   is_new = True if the User was just created
    if is_new:
        Profile.objects.get_or_create(user=user)
        #   Create a Profile for newly registered social auth users
        #   get_or_create avoids duplicates if the signal also fires
```

Run the development server over HTTPS (required by OAuth providers):

```bash
pip install django-extensions werkzeug pyOpenSSL
#   django-extensions provides the runserver_plus command
#   werkzeug + pyOpenSSL enable the HTTPS development server
```

```python
# settings.py
INSTALLED_APPS = [
    # ...
    'django_extensions',
    #   Provides management commands including runserver_plus
]
```

```bash
python manage.py runserver_plus --cert-file cert.crt 0.0.0.0:8000
#   Starts the development server with a self-signed SSL certificate
#   Your browser will show a security warning — click "Advanced" and proceed
#   OAuth providers require HTTPS for redirect URIs
```

Add the social login button to your template:

```html
<!-- templates/registration/login.html -->
{% extends "base.html" %}

{% block title %}Log In{% endblock %}

{% block content %}
<h2>Log In</h2>

<!-- Standard login form -->
<form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Log In</button>
</form>

<hr />

<!-- Social authentication -->
<h3>Or sign in with:</h3>
<a href="{% url 'social:begin' 'google-oauth2' %}" class="btn btn-google">
    Sign in with Google
</a>
<!--  'social:begin' starts the OAuth flow for the given backend  -->
<!--  Django redirects the user to Google's consent screen  -->
<!--  After authorization, Google redirects back to your callback URL  -->

<p>
    <a href="{% url 'password_reset' %}">Forgot your password?</a>
</p>
{% endblock %}
```

Add social auth context processors so templates can access social data:

```python
# settings.py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                # ... existing context processors ...
                'social_django.context_processors.backends',
                #   Makes social auth backends available in templates

                'social_django.context_processors.login_redirect',
                #   Provides the SOCIAL_AUTH_LOGIN_REDIRECT_URL in templates
            ],
        },
    },
]
```

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


### Redis

> 💡 **Analogy:** Think of Redis as a **whiteboard in your office** — it's incredibly fast to read and write because everything is right there in memory. Unlike a filing cabinet (MySQL), you don't need to open drawers and search through folders. But if someone erases the whiteboard (server restarts), the data is gone unless you took a photo (persistence). Redis adds special markers — sorted lists, counters, expiry timers — that a plain whiteboard can't do.

1️⃣ **WHY** — Redis is an in-memory data store that operates at sub-millisecond speed. It supports rich data structures (strings, hashes, lists, sets, sorted sets) beyond simple key-value pairs, making it ideal for caching, real-time counters, leaderboards, and session storage. Unlike Memcached, Redis can persist data to disk and supports atomic operations.

2️⃣ **WHEN** — Use Redis when you need lightning-fast reads/writes for counters (page views, likes), rankings/leaderboards (sorted sets), rate limiting, session storage, or as a full-featured cache backend for Django. It is the preferred choice over Memcached when you need data structures beyond simple strings.

3️⃣ **HOW**

**Installing Redis with Docker:**

```bash
# Pull and run Redis in a Docker container
docker pull redis
#   Downloads the latest Redis image from Docker Hub

docker run -d --name my-redis -p 6379:6379 redis
#   -d            → run in detached (background) mode
#   --name        → give the container a friendly name
#   -p 6379:6379  → map host port 6379 to container port 6379 (Redis default)

# Verify Redis is running
docker exec -it my-redis redis-cli ping
#   Should print "PONG" — confirms Redis is accepting connections
```

**Using Redis with Python (redis-py):**

```bash
pip install redis
#   Installs the official Python client for Redis
```

```python
import redis

# Connect to Redis
r = redis.Redis(host='localhost', port=6379, db=0)
#   host      → Redis server address
#   port      → default Redis port
#   db=0      → Redis supports 16 databases (0-15); 0 is the default

# Basic string operations
r.set('greeting', 'Hello Django!')
#   SET key value — stores a string value under the key 'greeting'

value = r.get('greeting')
#   GET key — retrieves the value; returns bytes: b'Hello Django!'

print(value.decode('utf-8'))
#   Decode bytes to a Python string: 'Hello Django!'

# Set a key with an expiration (TTL)
r.setex('temp_token', 300, 'abc123')
#   SETEX key seconds value — key expires automatically after 300 seconds (5 min)

# Check remaining time-to-live
ttl = r.ttl('temp_token')
#   Returns the number of seconds until the key expires
```

**Storing image/page views in Redis (counter pattern):**

```python
# views.py — track how many times each post is viewed
import redis
from django.shortcuts import get_object_or_404, render
from .models import Post

r = redis.Redis(host='localhost', port=6379, db=0)
#   Create a Redis connection (reuse across requests in production)

def post_detail(request, year, month, day, slug):
    post = get_object_or_404(
        Post,
        slug=slug,
        status='published',
        publish_date__year=year,
        publish_date__month=month,
        publish_date__day=day,
    )

    total_views = r.incr(f'post:{post.id}:views')
    #   INCR key — atomically increments the integer value by 1
    #   If the key doesn't exist, it's created with value 0 first
    #   Returns the new value — no race conditions even under heavy traffic
    #   Key format: "post:42:views" — use colons as namespace separators

    return render(request, 'blog/post_detail.html', {
        'post': post,
        'total_views': total_views,
        #   Pass the view count to the template
    })
```

**Storing a ranking in Redis (sorted sets):**

```python
# views.py — build a "most viewed posts" leaderboard
import redis
from django.shortcuts import get_object_or_404, render
from .models import Post

r = redis.Redis(host='localhost', port=6379, db=0)

def post_detail(request, year, month, day, slug):
    post = get_object_or_404(
        Post,
        slug=slug,
        status='published',
        publish_date__year=year,
        publish_date__month=month,
        publish_date__day=day,
    )

    total_views = r.incr(f'post:{post.id}:views')
    #   Increment the individual view counter

    r.zincrby('post_ranking', 1, post.id)
    #   ZINCRBY key increment member
    #   Adds 1 to the score of this post in the sorted set 'post_ranking'
    #   Sorted sets automatically keep members ordered by score

    return render(request, 'blog/post_detail.html', {
        'post': post,
        'total_views': total_views,
    })


def post_ranking(request):
    post_ranking_ids = r.zrange('post_ranking', 0, -1, desc=True)[:10]
    #   ZRANGE key start stop [DESC]
    #   Returns members ordered by score; desc=True → highest scores first
    #   [:10] → take only the top 10 post IDs

    post_ranking_ids = [int(id) for id in post_ranking_ids]
    #   Redis returns bytes — convert to integers for Django ORM lookup

    most_viewed = list(Post.objects.filter(id__in=post_ranking_ids))
    #   Fetch the Post objects from MySQL for the top-ranked IDs

    most_viewed.sort(key=lambda x: post_ranking_ids.index(x.id))
    #   Re-sort Python list to match Redis ranking order
    #   (Django QuerySet doesn't guarantee order matches the IN list)

    return render(request, 'blog/post_ranking.html', {
        'most_viewed': most_viewed,
    })
```

**Using Redis with Django (django-redis):**

```bash
pip install django-redis
#   Provides a Django cache backend powered by Redis
#   Lets you use Django's cache framework with Redis under the hood
```

```python
# settings.py — configure Redis as Django's cache backend
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        #   Django 4.0+ includes a built-in Redis cache backend
        #   For older versions, use 'django_redis.cache.RedisCache'

        'LOCATION': 'redis://127.0.0.1:6379/1',
        #   redis://host:port/db_number
        #   Using db=1 to separate cache data from other Redis usage (db=0)
    }
}

# Optional: use Redis for session storage too
SESSION_ENGINE = 'django.contrib.sessions.backends.cache'
#   Store sessions in the cache backend (Redis) instead of the database
SESSION_CACHE_ALIAS = 'default'
#   Use the 'default' cache (Redis) for sessions
```

```python
# Using Django's cache API (backed by Redis)
from django.core.cache import cache

# This now reads/writes to Redis transparently
cache.set('my_key', 'my_value', timeout=60 * 15)
#   Stores 'my_value' in Redis with a 15-minute TTL

value = cache.get('my_key')
#   Retrieves the value from Redis — returns None if expired or missing
```

---

### Memcached

> 💡 **Analogy:** Memcached is like a **coat check at a theater** — you hand over your coat (data), get a ticket (key), and retrieve it later instantly. It's simple, fast, and purpose-built for one job: temporary storage. It doesn't sort your coats, count them, or remember them after closing time. Redis, by contrast, is a full cloakroom with numbered shelves, a logbook, and overnight storage.

1️⃣ **WHY** — Memcached is a high-performance, distributed memory caching system. It reduces database load by storing frequently accessed data in RAM. Memcached is battle-tested, extremely simple, and handles multi-threaded workloads well. Django has built-in support for Memcached as a cache backend.

2️⃣ **WHEN** — Use Memcached when you need a simple, fast, distributed cache and don't need the advanced data structures (sorted sets, lists, pub/sub) that Redis provides. Memcached is a good fit when your caching needs are straightforward key-value pairs with expiration.

3️⃣ **HOW**

**Installing Memcached with Docker:**

```bash
# Pull and run Memcached in a Docker container
docker pull memcached
#   Downloads the latest Memcached image from Docker Hub

docker run -d --name my-memcached -p 11211:11211 memcached
#   -d             → run in detached (background) mode
#   --name         → give the container a friendly name
#   -p 11211:11211 → map host port to container port (Memcached default)

# Verify Memcached is running
echo "stats" | nc localhost 11211
#   Should print server statistics — confirms Memcached is accepting connections
```

**Installing the Python binding (pymemcache):**

```bash
pip install pymemcache
#   pymemcache is the recommended Python client for Memcached
#   It is pure Python, actively maintained, and used by Django internally
```

**Configuring Django to use Memcached:**

```python
# settings.py — configure Memcached as Django's cache backend
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.PyMemcacheCache',
        #   Uses pymemcache under the hood
        #   Django also supports PyLibMCCache (using pylibmc C extension)

        'LOCATION': '127.0.0.1:11211',
        #   host:port of your Memcached server
    }
}

# For multiple Memcached servers (distributed caching):
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.memcached.PyMemcacheCache',
        'LOCATION': [
            '172.19.26.240:11211',
            '172.19.26.242:11211',
            #   Requests are distributed across servers using consistent hashing
            #   If one server goes down, only its keys are lost — not the whole cache
        ],
    }
}
```

```python
# Using the cache (works the same regardless of backend)
from django.core.cache import cache

cache.set('categories', list(Category.objects.all()), timeout=60 * 60)
#   Store the categories list for 1 hour
#   Memcached serializes objects using pickle by default

categories = cache.get('categories')
#   Returns the cached list, or None if expired/missing

cache.delete('categories')
#   Explicitly remove a key (useful after updating category data)
```

**Memcached vs Redis — quick comparison:**

```text
Feature              Memcached               Redis
─────────────────    ──────────────────────   ──────────────────────
Data types           Strings only             Strings, lists, sets,
                                              sorted sets, hashes
Persistence          None (RAM only)          Optional (RDB/AOF)
Threading            Multi-threaded           Single-threaded (fast)
Max value size       1 MB default             512 MB default
Pub/Sub              No                       Yes
Atomic operations    incr/decr only           Rich command set
Django built-in      Yes                      Yes (Django 4.0+)
Best for             Simple key-value cache   Cache + data structures
```

---

### Cache Levels

> 💡 **Analogy:** Think of Django's cache levels like **layers of a postal system**. The **low-level cache API** is like personally handing a letter to someone (precise, targeted). **Template fragment caching** is like pre-printing a common section of a newsletter. **Per-view caching** is like photocopying an entire letter for everyone who asks for it. **Per-site caching** is like printing the whole newspaper once and handing out copies — the fastest, broadest approach but the least flexible.

1️⃣ **WHY** — Different parts of your application have different caching needs. A user dashboard might change every request, but a sidebar "Top Posts" widget can be cached for hours. Django provides four levels of caching granularity so you can cache precisely what makes sense.

2️⃣ **WHEN** — Use the low-level API for fine-grained control over individual data. Use template fragment caching for expensive template blocks. Use per-view caching for entire pages that are the same for all users. Use per-site caching when most pages on your site can be cached.

3️⃣ **HOW**

**Level 1 — Low-level cache API:**

```python
from django.core.cache import cache

# Basic get/set pattern
cache.set('total_posts', Post.objects.count(), timeout=60 * 10)
#   Store the post count for 10 minutes
#   timeout=None → cache forever (until evicted or manually deleted)

total = cache.get('total_posts')
#   Returns the cached value, or None if the key doesn't exist

total = cache.get('total_posts', default=0)
#   Returns 0 instead of None when the key is missing

# get_or_set — fetch from cache or compute and store in one call
total = cache.get_or_set('total_posts', Post.objects.count(), timeout=60 * 10)
#   If 'total_posts' exists in cache → return it
#   If not → call Post.objects.count(), store the result, and return it
#   This is the preferred pattern — avoids the if/else boilerplate

# Versioning — useful for cache invalidation
cache.set('sidebar_html', rendered_html, version=2)
#   Stores under version 2 of the key
cache.get('sidebar_html', version=2)
#   Only retrieves version 2 — version 1 is effectively expired

# Increment / decrement (atomic operations)
cache.set('page_hits', 0)
cache.incr('page_hits')
#   Atomically increment by 1 — safe under concurrent requests
cache.incr('page_hits', delta=10)
#   Increment by 10

# Delete and clear
cache.delete('total_posts')
#   Remove a single key
cache.clear()
#   Remove ALL keys from the cache — use with caution!

# set_many / get_many — batch operations for efficiency
cache.set_many({'key1': 'val1', 'key2': 'val2'}, timeout=300)
#   Store multiple keys in a single round-trip to the cache server
result = cache.get_many(['key1', 'key2'])
#   Returns a dict: {'key1': 'val1', 'key2': 'val2'}
#   Missing keys are omitted from the result
```

**Level 2 — Template fragment caching:**

```html
<!-- Load the cache template tag library -->
{% load cache %}

<!-- Cache the sidebar for 15 minutes -->
{% cache 900 sidebar %}
    <!--
        {% cache timeout fragment_name %}
        900         → timeout in seconds (15 minutes)
        sidebar     → unique name for this fragment
    -->
    <div class="sidebar">
        <h3>Popular Posts</h3>
        {% for post in popular_posts %}
            <a href="{{ post.get_absolute_url }}">{{ post.title }}</a>
        {% endfor %}
    </div>
{% endcache %}

<!-- Cache per user — pass a variable to make the key unique -->
{% cache 600 user_dashboard request.user.id %}
    <!--
        The cache key includes request.user.id
        So each user gets their own cached version
    -->
    <p>Welcome back, {{ request.user.username }}!</p>
    <p>You have {{ unread_count }} unread messages.</p>
{% endcache %}
```

**Level 3 — Per-view caching with `@cache_page`:**

```python
# views.py — cache the entire HTTP response for a view
from django.views.decorators.cache import cache_page

@cache_page(60 * 15)
#   Cache the rendered response for 15 minutes (900 seconds)
#   The cache key includes the full URL, so /posts/?page=1 and /posts/?page=2
#   are cached separately
def post_list(request):
    posts = Post.objects.filter(status='published').order_by('-publish_date')
    return render(request, 'blog/post_list.html', {'posts': posts})
```

```python
# urls.py — alternative: apply cache_page in URL configuration
from django.views.decorators.cache import cache_page
from . import views

urlpatterns = [
    path(
        'posts/',
        cache_page(60 * 15)(views.post_list),
        #   Same effect as the decorator, but keeps the view clean
        #   Useful when you don't control the view code (e.g., third-party views)
        name='post_list',
    ),
]
```

```python
# Using cache_page with class-based views
from django.views.decorators.cache import cache_page
from django.utils.decorators import method_decorator
from django.views.generic import ListView
from .models import Post

@method_decorator(cache_page(60 * 15), name='dispatch')
#   For CBVs, decorate the 'dispatch' method
#   This caches the entire response regardless of HTTP method
class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'
    queryset = Post.objects.filter(status='published')
    paginate_by = 10
```

**Level 4 — Per-site caching (cache everything):**

```python
# settings.py — enable site-wide caching via middleware
MIDDLEWARE = [
    'django.middleware.cache.UpdateCacheMiddleware',
    #   MUST be first — sets cache headers on the response
    #   Processes the response AFTER the view runs

    'django.middleware.common.CommonMiddleware',
    #   ... other middleware ...

    'django.middleware.cache.FetchFromCacheMiddleware',
    #   MUST be last — checks if a cached response exists
    #   Processes the request BEFORE the view runs
    #   If a cached response is found, the view is never called
]

CACHE_MIDDLEWARE_ALIAS = 'default'
#   Which cache backend to use (from the CACHES setting)

CACHE_MIDDLEWARE_SECONDS = 600
#   Default cache timeout: 10 minutes for every page

CACHE_MIDDLEWARE_KEY_PREFIX = 'mysite'
#   Prefix for cache keys — prevents collisions if multiple Django sites
#   share the same cache server
```

```python
# To exclude specific views from site-wide caching:
from django.views.decorators.cache import never_cache

@never_cache
#   This view will never be cached, even with per-site caching enabled
#   Useful for user-specific pages, CSRF-protected forms, etc.
def user_dashboard(request):
    return render(request, 'dashboard.html', {'user': request.user})
```

---

### Django Debug Toolbar

> 💡 **Analogy:** Django Debug Toolbar is like a **car's diagnostic dashboard** — it shows you engine RPM (SQL queries), fuel consumption (memory usage), tire pressure (template rendering), and warning lights (cache misses) all while you're driving (developing). Without it, you're guessing what's wrong under the hood.

1️⃣ **WHY** — Django Debug Toolbar provides detailed information about how each page is generated: the SQL queries executed, templates rendered, cache hits/misses, signals fired, HTTP headers, and more. It is the single most important tool for identifying performance bottlenecks (especially N+1 queries) during development.

2️⃣ **WHEN** — Install it immediately in every Django project. Use it during development to inspect query counts, duplicate queries, and slow queries. It should **never** be enabled in production because it exposes internal application details.

3️⃣ **HOW**

**Installing Django Debug Toolbar:**

```bash
pip install django-debug-toolbar
#   Installs the toolbar and its dependencies
```

**Configuring Django Debug Toolbar:**

```python
# settings.py — add debug toolbar to your project

INSTALLED_APPS = [
    # ... existing apps ...
    'debug_toolbar',
    #   Register the debug toolbar application
]

MIDDLEWARE = [
    'debug_toolbar.middleware.DebugToolbarMiddleware',
    #   Should be placed as early as possible in the middleware list
    #   (but after any middleware that encodes the response, like GZipMiddleware)
    # ... other middleware ...
]

INTERNAL_IPS = [
    '127.0.0.1',
    #   The toolbar only appears for requests from these IP addresses
    #   This prevents it from showing up for other users on a shared server
]

# Optional: explicit toolbar configuration
DEBUG_TOOLBAR_CONFIG = {
    'SHOW_TOOLBAR_CALLBACK': lambda request: DEBUG,
    #   Only show the toolbar when DEBUG=True
    #   You can customize this with a function for more complex logic
}
```

```python
# urls.py (project-level) — add debug toolbar URLs
from django.conf import settings
from django.urls import include, path

urlpatterns = [
    # ... your existing URL patterns ...
]

if settings.DEBUG:
    import debug_toolbar
    urlpatterns = [
        path('__debug__/', include(debug_toolbar.urls)),
        #   Serves the toolbar's static assets and AJAX endpoints
        #   Only included when DEBUG=True — never exposed in production
    ] + urlpatterns
```

**Available panels:**

```text
Panel              What it shows
─────────────────  ──────────────────────────────────────────────────
History            Previous requests and their debug data
Versions           Django version and installed package versions
Timer              Total request/response time and CPU time
Settings           All Django settings (with sensitive values hidden)
Headers            HTTP request and response headers
Request            View function, URL route, cookies, session data
SQL                Every SQL query, execution time, and EXPLAIN output
Static files       Static files loaded for the page
Templates          Templates rendered and their context variables
Cache              Cache calls: get, set, delete, hits, and misses
Signals            Django signals fired during the request
Logging            Log messages generated during the request
Profiling          Python cProfile output for the request (optional)
```

**Using the SQL panel to identify N+1 queries:**

```python
# Example: a view that triggers N+1 queries
# views.py
def post_list(request):
    posts = Post.objects.filter(status='published')
    #   Query 1: SELECT * FROM blog_post WHERE status='published'
    return render(request, 'blog/post_list.html', {'posts': posts})
```

```html
<!-- blog/post_list.html -->
{% for post in posts %}
    <h2>{{ post.title }}</h2>
    <p>By {{ post.author.username }}</p>
    <!--
        Each iteration triggers a SEPARATE query:
        Query 2: SELECT * FROM auth_user WHERE id=1
        Query 3: SELECT * FROM auth_user WHERE id=2
        ... and so on — one query per post!
    -->
    <p>Category: {{ post.category.name }}</p>
    <!--
        Even MORE queries for category:
        Query N+1: SELECT * FROM blog_category WHERE id=...
    -->
{% endfor %}
```

```text
What the SQL panel shows for 20 posts:
──────────────────────────────────────────────────
41 queries in 28.5ms

  SELECT ... FROM blog_post WHERE status='published'               1.2ms
  SELECT ... FROM auth_user WHERE id=3                             0.4ms  ← DUPLICATE
  SELECT ... FROM auth_user WHERE id=3                             0.4ms  ← DUPLICATE
  SELECT ... FROM blog_category WHERE id=1                         0.3ms  ← DUPLICATE
  ...
  (repeated queries highlighted in red by the toolbar)

The toolbar highlights:
  • Total query count (41 is way too many for a list page)
  • Duplicate queries (same SQL executed multiple times)
  • Time per query and total SQL time
  • Click any query to see its full SQL and EXPLAIN plan
```

```python
# The fix — use select_related to eliminate N+1 queries
def post_list(request):
    posts = Post.objects.filter(
        status='published'
    ).select_related(
        'author',      # JOIN auth_user
        'category',    # JOIN blog_category
    )
    #   Now: 1 query with JOINs instead of 41 separate queries
    #   The SQL panel will show: "1 query in 1.8ms"
    return render(request, 'blog/post_list.html', {'posts': posts})
```

**Debug Toolbar management commands:**

```bash
python manage.py debugsqlshell
#   Opens a Python shell that prints the SQL for every ORM operation
#   Useful for inspecting queries without opening a browser

# Example session:
# >>> from blog.models import Post
# >>> Post.objects.filter(status='published').count()
# SELECT COUNT(*) FROM "blog_post" WHERE "blog_post"."status" = 'published'
# 42
```

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

Consuming the API:

```bash
# List all posts (GET)
curl http://127.0.0.1:8000/api/posts/
#   Returns JSON array of published posts

# Retrieve a single post (GET)
curl http://127.0.0.1:8000/api/posts/1/
#   Returns JSON object for post with id=1

# Create a post (POST — requires authentication)
curl -X POST http://127.0.0.1:8000/api/posts/ \
     -H "Content-Type: application/json" \
     -u admin:password123 \
     -d '{"title": "New Post", "body": "Hello from the API", "status": "published"}'
#   -u → HTTP Basic Authentication (username:password)
#   -d → JSON request body

# Using Python requests library
import requests
response = requests.get('http://127.0.0.1:8000/api/posts/')
posts = response.json()
#   .json() → parses the JSON response into a Python list/dict
```

> **Tip:** DRF includes a **browsable API** — visit `/api/posts/` in your browser to see an interactive HTML interface where you can test endpoints, submit forms, and inspect responses without writing any client code.

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
#   Alternative: RabbitMQ → 'amqp://guest:guest@localhost:5672//'
#   RabbitMQ is a dedicated message broker with advanced routing features
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


#### Rosetta Translation Interface

Editing `.po` files by hand is tedious. **django-rosetta** provides a web-based interface for translators to edit translations directly in the browser.

Install and configure Rosetta:

```bash
pip install django-rosetta
#   Installs the Rosetta translation interface package
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'rosetta',
    #   Adds the Rosetta translation interface to your project
]
```

```python
# urls.py (project-level)
from django.urls import path, include

urlpatterns = [
    ...
    path('rosetta/', include('rosetta.urls')),
    #   Mounts the Rosetta interface at /rosetta/
    #   Only staff users can access it by default
]
```

Navigate to `http://localhost:8000/rosetta/` in your browser. Rosetta displays all available `.po` files grouped by application. Click a language to see the list of translatable strings.

For each string you will see the original text and a text field for the translation. Rosetta saves changes directly to the `.po` file and compiles the `.mo` file automatically.

**Fuzzy translations** are strings that `makemessages` has flagged as uncertain — usually because the source string changed slightly and Django guessed a match. Rosetta highlights fuzzy entries so translators can review and confirm or correct them:

```python
# Inside the .po file, a fuzzy entry looks like this:
#, fuzzy
msgid "Add new item to cart"
msgstr "Añadir artículo al carrito"
#   The fuzzy flag tells Django to ignore this translation until
#   a translator reviews it and removes the flag
```

> ⚠️ **Tip:** Restrict Rosetta access in production. Add `ROSETTA_REQUIRES_AUTH = True` in your settings so only authenticated staff users can edit translations.

```python
# settings.py
ROSETTA_REQUIRES_AUTH = True
#   Ensures only logged-in staff users can access Rosetta
ROSETTA_STORAGE_CLASS = 'rosetta.storage.CacheRosettaStorage'
#   Uses Django's cache backend to store Rosetta session data
```

✏️ **Practice:** Install Rosetta, open the Spanish `.po` file through the web interface, translate five strings, and verify the translations appear on the site without running `compilemessages` manually.

---

#### Translating Models with django-parler

Marking field labels with `gettext_lazy` translates the **interface** but not the **content** stored in MySQL. **django-parler** stores translated versions of model fields in separate database tables.

```bash
pip install django-parler
```
```python
# settings.py
INSTALLED_APPS = [
    ...
    'parler',                       #   Enables model-level translations
]
PARLER_LANGUAGES = {
    None: ({'code': 'en'}, {'code': 'es'}),
    'default': {'fallback': 'en'},  #   Fall back to English if translation is missing
}
```

Define a translated model and run the migration:

```python
# shop/models.py
from django.db import models
from parler.models import TranslatableModel, TranslatedFields

class Product(TranslatableModel):
    #   TranslatableModel → base class that adds translation support
    sku = models.CharField(max_length=50, unique=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    translations = TranslatedFields(
        name=models.CharField(max_length=200),
        #   Translated field — stored per language in a separate table
        description=models.TextField(),
    )
```
```bash
python manage.py makemigrations shop && python manage.py migrate
#   Creates the shop_product_translation table in MySQL
```

Query translated content:

```python
from django.utils.translation import activate
activate('es')                                              #   Switch to Spanish
product = Product.objects.language('es').get(sku='WIDGET-01')
#   language('es') → fetches the Spanish translation row
```
```python
# shop/admin.py
from parler.admin import TranslatableAdmin
from .models import Product

@admin.register(Product)
class ProductAdmin(TranslatableAdmin):
    #   TranslatableAdmin → adds language tabs in the admin form
    list_display = ['sku', 'name', 'price']
```

✏️ **Practice:** Add translated fields to a Product model, create the migration, add English and Spanish content through the admin, and verify switching languages displays the correct text.

---

#### Format Localization

Django can automatically format **dates**, **times**, **numbers**, and **currencies** according to the active locale, so users see formats they are familiar with.

```python
# settings.py
USE_L10N = True
#   Activates locale-aware formatting for dates and numbers
#   With this enabled, Django uses locale-specific formats automatically

USE_TZ = True
#   Stores datetimes in UTC; displays them in the user's time zone
```

When `USE_L10N = True`, Django formats values based on the active language. For example, the number `1234567.89` displays as:

- English (en): `1,234,567.89`
- Spanish (es): `1.234.567,89`
- French (fr): `1 234 567,89`

Use the `localize` filter in templates to format individual values:

```html
{% load l10n %}
{# Load the localization template filters #}

<p>Price: {{ product.price|localize }}</p>
{# localize → formats the number according to the active locale #}

<p>Published: {{ post.publish_date|localize }}</p>
{# Dates are also formatted: 12/31/2025 (en) vs 31/12/2025 (es) #}
```

You can disable localization for a specific block when you need machine-readable output:

```html
{% load l10n %}

{% localize off %}
    <input type="hidden" name="raw_price" value="{{ product.price }}">
    {# Inside {% localize off %}, values render without locale formatting #}
    {# Useful for hidden form fields or JavaScript data attributes #}
{% endlocalize %}
```

To override the default format for a specific locale, create a custom format file:

```python
# locale/es/formats.py
DATE_FORMAT = 'd de F de Y'
#   Overrides the default Spanish date format
#   Example output: "31 de diciembre de 2025"

DECIMAL_SEPARATOR = ','
THOUSAND_SEPARATOR = '.'
#   Confirms the Spanish number formatting convention
```

✏️ **Practice:** Enable `USE_L10N`, display a product price and a publish date in a template, then switch between English, Spanish, and French to observe how the formatting changes automatically.

---

#### Validating Form Fields with django-localflavor

**django-localflavor** provides country-specific form fields and validators — postal codes, state selectors, national ID numbers, and more.

Install django-localflavor:

```bash
pip install django-localflavor
#   Installs locale-specific form fields and validators
```

Use US-specific fields in a form:

```python
# shop/forms.py
from django import forms
from localflavor.us.forms import USStateField, USZipCodeField
#   USStateField → dropdown of US state abbreviations (CA, NY, TX, …)
#   USZipCodeField → validates US ZIP codes (12345 or 12345-6789)

class ShippingAddressForm(forms.Form):
    name = forms.CharField(max_length=100)
    address = forms.CharField(max_length=200)
    city = forms.CharField(max_length=100)

    state = USStateField()
    #   Renders as a select widget with all US states and territories
    zip_code = USZipCodeField()
    #   Validates the input matches a 5-digit or 9-digit US ZIP format
```

Fields for other countries work the same way:

```python
# Using Spanish-specific fields
from localflavor.es.forms import ESIdentityCardNumberField, ESPostalCodeField

class SpanishCustomerForm(forms.Form):
    dni = ESIdentityCardNumberField()
    #   Validates a Spanish DNI, NIE, or NIF identity number
    postal_code = ESPostalCodeField()
    #   Validates a 5-digit Spanish postal code (01000–52999)
```

Combine localflavor with a ModelForm to validate before saving to MySQL:

```python
# shop/forms.py
from .models import ShippingAddress

class ShippingAddressModelForm(forms.ModelForm):
    state = USStateField()
    #   Overrides the default CharField with a US state selector
    zip_code = USZipCodeField()
    #   Adds ZIP code validation on top of the model field

    class Meta:
        model = ShippingAddress
        fields = ['name', 'address', 'city', 'state', 'zip_code']
```

✏️ **Practice:** Create a checkout form that uses `USStateField` and `USZipCodeField`. Submit the form with an invalid ZIP code (e.g., "ABCDE") and verify the validation error appears.

---

#### URL Patterns for Internationalization

Django can **prefix URLs with the language code** (e.g., `/en/blog/`, `/es/blog/`) and **translate URL path segments** so that `/es/publicaciones/` maps to the same view as `/en/posts/`.

```python
# urls.py (project-level)
from django.conf.urls.i18n import i18n_patterns

urlpatterns = [
    path('i18n/', include('django.conf.urls.i18n')),
    #   Mounts the set_language view at /i18n/setlang/
]
urlpatterns += i18n_patterns(
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls', namespace='blog')),
    #   URLs become /en/admin/, /es/admin/, /en/blog/, /es/blog/, etc.
)
```

Translate URL path segments with `gettext_lazy` and add the translation in your `.po` file:

```python
# blog/urls.py
from django.utils.translation import gettext_lazy as _
from django.urls import path
from . import views

app_name = 'blog'
urlpatterns = [
    path(_('posts/'), views.post_list, name='post_list'),
    #   _('posts/') → translatable: /en/blog/posts/ or /es/blog/publicaciones/
    path(_('posts/<int:pk>/'), views.post_detail, name='post_detail'),
]
```

```text
# locale/es/LC_MESSAGES/django.po
msgid "posts/"
msgstr "publicaciones/"
```

Add a language switcher dropdown to your template:

```html
{# templates/base.html #}
{% load i18n %}
<form action="{% url 'set_language' %}" method="post">
    {% csrf_token %}
    <input type="hidden" name="next" value="{{ request.path }}">
    {# next → redirects back to the current page after switching #}
    <select name="language" onchange="this.form.submit()">
        {% get_available_languages as languages %}
        {% for lang_code, lang_name in languages %}
            <option value="{{ lang_code }}"
                {% if lang_code == LANGUAGE_CODE %}selected{% endif %}>
                {{ lang_name }}
            </option>
        {% endfor %}
    </select>
</form>
```

Django stores the language preference in the session and redirects to the translated URL.

✏️ **Practice:** Wrap your blog URLs with `i18n_patterns`, translate the `posts/` segment into Spanish, add the language switcher to your base template, and verify that switching languages changes both the prefix and the path.



### Sitemaps

> 💡 **Analogy:** A sitemap is like the **index at the back of a textbook** — it tells search engines exactly which pages exist and where to find them, so they can crawl your site efficiently instead of wandering around hoping to discover every page.

1️⃣ **WHY** — Sitemaps help search engines discover and index your content faster. Without a sitemap, a crawler must follow links to find pages, which means deep or orphaned pages may never be indexed. Django's sitemap framework generates `sitemap.xml` automatically from your models.

2️⃣ **WHEN** — Every public-facing site benefits from a sitemap, but they are especially important for content-heavy sites (blogs, news, e-commerce) where new pages are added frequently and SEO matters.

3️⃣ **HOW**

Enable the sitemaps framework in `settings.py`:

```python
# settings.py
INSTALLED_APPS = [
    ...
    'django.contrib.sites',
    #   Required by the sitemap framework to generate absolute URLs
    'django.contrib.sitemaps',
    #   The sitemap framework itself
]

SITE_ID = 1
#   Identifies which Site object to use for building absolute URLs
```

Create a sitemap class for your blog posts:

```python
# blog/sitemaps.py
from django.contrib.sitemaps import Sitemap
from .models import Post

class PostSitemap(Sitemap):
    changefreq = 'weekly'
    #   Hint to crawlers: pages change about once a week
    priority = 0.9
    #   Priority relative to other pages on the site (0.0 to 1.0)

    def items(self):
        """Return the queryset of objects to include in the sitemap."""
        return Post.objects.filter(status='published')
        #   Only published posts should appear in the sitemap

    def lastmod(self, obj):
        """Return the last modification date for each object."""
        return obj.updated_at
        #   Tells crawlers when the page was last changed
```

Register the sitemap in your URL configuration:

```python
# mysite/urls.py
from django.contrib.sitemaps.views import sitemap
from blog.sitemaps import PostSitemap

sitemaps = {
    'posts': PostSitemap,
    #   Key becomes the <loc> section name in the sitemap index
}

urlpatterns = [
    ...
    path('sitemap.xml', sitemap, {'sitemaps': sitemaps},
         name='django.contrib.sitemaps.views.sitemap'),
    #   Visiting /sitemap.xml now returns a valid XML sitemap
]
```

The generated `sitemap.xml` output looks like this:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://example.com/blog/2024/01/15/my-first-post/</loc>
    <lastmod>2024-01-20</lastmod>
    <changefreq>weekly</changefreq>
    <priority>0.9</priority>
  </url>
  <!-- One <url> entry per published post -->
</urlset>
```

After deploying, submit your sitemap URL to Google Search Console and Bing Webmaster Tools so crawlers pick it up immediately.

---

### RSS Feeds

> 💡 **Analogy:** An RSS feed is like a **newspaper subscription** — instead of visiting the website every day to check for new articles, readers subscribe once and new content is delivered to their feed reader automatically.

1️⃣ **WHY** — RSS feeds let users and aggregators follow your content without repeatedly visiting your site. Django's syndication framework generates valid RSS (or Atom) feeds from your models with minimal code.

2️⃣ **WHEN** — Any site that publishes content over time — blogs, news sites, podcasts, changelogs — should offer an RSS feed. It is also useful for inter-system communication where a lightweight pull-based protocol is sufficient.

3️⃣ **HOW**

Create a feed class for your blog:

```python
# blog/feeds.py
from django.contrib.syndication.views import Feed
from django.template.defaultfilters import truncatewords
from .models import Post

class LatestPostsFeed(Feed):
    title = 'My Blog'
    #   The <title> element in the RSS XML
    link = '/blog/'
    #   The <link> pointing back to your site
    description = 'New posts on my blog.'
    #   The <description> element shown in feed readers

    def items(self):
        """Return the objects to include as feed entries."""
        return Post.objects.filter(status='published')[:5]
        #   Latest 5 published posts

    def item_title(self, item):
        """Return the title for each feed entry."""
        return item.title

    def item_description(self, item):
        """Return a summary for each feed entry."""
        return truncatewords(item.body, 30)
        #   Show the first 30 words of the post body

    def item_pubdate(self, item):
        """Return the publication date for each entry."""
        return item.publish_date
        #   Maps to <pubDate> in the RSS output
```

Register the feed in your URL configuration:

```python
# blog/urls.py
from .feeds import LatestPostsFeed

urlpatterns = [
    ...
    path('feed/', LatestPostsFeed(), name='post_feed'),
    #   /blog/feed/ now serves a valid RSS 2.0 XML document
]
```

Add a link in your base template so browsers auto-discover the feed:

```html
<!-- templates/base.html -->
<head>
    ...
    <link rel="alternate" type="application/rss+xml"
          title="My Blog RSS Feed"
          href="{% url 'blog:post_feed' %}">
    <!-- Browsers and feed readers detect this <link> automatically -->
</head>
```

Users can paste `/blog/feed/` into any RSS reader (Feedly, Inoreader, NetNewsWire) to subscribe.

---

### Full-Text Search

> 💡 **Analogy:** Simple `LIKE` queries are like searching a book by flipping through every page. Full-text search is like using the book's **index and glossary** — it understands word forms, ranks results by relevance, and finds matches far faster.

1️⃣ **WHY** — Basic `icontains` lookups perform a `LIKE '%term%'` scan, which is slow on large tables and returns no relevance ranking. Full-text search uses inverted indexes to match words efficiently, handle stemming (finding "running" when searching "run"), and rank results.

2️⃣ **WHEN** — Any time users need to search content — blog posts, products, documentation. If your site has more than a few hundred records, full-text search dramatically improves both speed and result quality.

3️⃣ **HOW**

**Simple search with `icontains` (works on any database including MySQL):**

```python
# blog/views.py — basic approach
def post_search(request):
    query = request.GET.get('q', '')
    results = []
    if query:
        results = Post.objects.filter(
            status='published',
            body__icontains=query,
            #   Case-insensitive LIKE '%query%' — works but no ranking
        )
    return render(request, 'blog/search.html', {
        'query': query,
        'results': results,
    })
```

**PostgreSQL full-text search with `SearchVector` and `SearchQuery`:**

```python
# blog/views.py — PostgreSQL approach
from django.contrib.postgres.search import (
    SearchVector, SearchQuery, SearchRank
)

def post_search(request):
    query = request.GET.get('q', '')
    results = []
    if query:
        search_vector = SearchVector('title', weight='A') + \
                        SearchVector('body', weight='B')
        #   weight='A' → highest importance, 'B' → second highest
        search_query = SearchQuery(query)
        #   Parses the user query and applies stemming automatically
        results = Post.objects.filter(status='published') \
            .annotate(
                search=search_vector,
                rank=SearchRank(search_vector, search_query),
                #   rank → relevance score based on term frequency
            ) \
            .filter(search=search_query) \
            .order_by('-rank')
            #   Most relevant results first
    return render(request, 'blog/search.html', {
        'query': query,
        'results': results,
    })
```

**Trigram similarity (PostgreSQL — requires `pg_trgm` extension):**

```python
# blog/views.py — fuzzy matching for typos
from django.contrib.postgres.search import TrigramSimilarity

results = Post.objects.filter(status='published') \
    .annotate(
        similarity=TrigramSimilarity('title', query),
        #   Compares character trigrams — catches misspellings
    ) \
    .filter(similarity__gt=0.1) \
    .order_by('-similarity')
```

**MySQL FULLTEXT search alternative:**

```sql
-- MySQL: create a FULLTEXT index (run via a migration or raw SQL)
ALTER TABLE blog_post ADD FULLTEXT INDEX ft_post (title, body);
```

```python
# blog/views.py — MySQL FULLTEXT approach
from django.db import connection

def post_search_mysql(request):
    query = request.GET.get('q', '')
    results = []
    if query:
        results = Post.objects.filter(status='published').extra(
            where=["MATCH(title, body) AGAINST(%s IN BOOLEAN MODE)"],
            params=[query],
            #   MySQL FULLTEXT search with boolean mode for +/- operators
        )
    return render(request, 'blog/search.html', {
        'query': query,
        'results': results,
    })
```

For MySQL, you can also use `RawSQL` or raw queries for full control over `MATCH ... AGAINST` syntax, including natural language mode and query expansion.

---

### Sending Emails

> 💡 **Analogy:** Django's email framework is like a **post office API** — you write the letter (message), address it (recipient), and hand it to the post office (backend). You can swap the post office for a local printer (console backend) during development without changing your letter-writing code.

1️⃣ **WHY** — Almost every web application needs to send emails — password resets, order confirmations, notifications, contact forms. Django provides a clean abstraction over SMTP so your view code stays simple while the delivery mechanism is configurable.

2️⃣ **WHEN** — Use `send_mail()` for simple one-off emails and `EmailMessage` when you need attachments, CC/BCC, or HTML content. Configure a console or file backend during development so you don't actually send emails while testing.

3️⃣ **HOW**

Configure email settings using environment variables for security:

```python
# settings.py
import os

EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
#   Use SMTP for production; swap to console backend for development
EMAIL_HOST = os.environ.get('EMAIL_HOST', 'smtp.gmail.com')
#   SMTP server hostname
EMAIL_PORT = int(os.environ.get('EMAIL_PORT', 587))
#   587 for TLS, 465 for SSL
EMAIL_USE_TLS = True
#   Encrypt the connection with TLS
EMAIL_HOST_USER = os.environ.get('EMAIL_HOST_USER')
#   Your email address — never hardcode this
EMAIL_HOST_PASSWORD = os.environ.get('EMAIL_HOST_PASSWORD')
#   App password or SMTP password — never commit to version control
DEFAULT_FROM_EMAIL = os.environ.get('DEFAULT_FROM_EMAIL', 'noreply@example.com')
```

For development, use the console backend to print emails to the terminal:

```python
# settings.py (development override)
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
#   Prints the full email to stdout instead of sending it
```

Send a simple email using `send_mail()`:

```python
# blog/views.py
from django.core.mail import send_mail
from django.shortcuts import render, get_object_or_404

def share_post_by_email(request, post_id):
    post = get_object_or_404(Post, id=post_id, status='published')
    sent = False
    if request.method == 'POST':
        form = EmailPostForm(request.POST)
        if form.is_valid():
            cd = form.cleaned_data
            post_url = request.build_absolute_uri(post.get_absolute_url())
            #   Build the full URL including domain
            subject = f'{cd["name"]} recommends: {post.title}'
            message = (
                f'Read "{post.title}" at {post_url}\n\n'
                f'{cd["name"]}\'s comments: {cd["comments"]}'
            )
            send_mail(subject, message, cd['email'], [cd['to']])
            #   send_mail(subject, body, from_email, recipient_list)
            sent = True
    else:
        form = EmailPostForm()
    return render(request, 'blog/share.html', {
        'post': post, 'form': form, 'sent': sent,
    })
```

For more control, use `EmailMessage` directly:

```python
# Sending an email with an attachment
from django.core.mail import EmailMessage

email = EmailMessage(
    subject='Your Invoice',
    body='Please find your invoice attached.',
    from_email='billing@example.com',
    to=['customer@example.com'],
    #   to → list of recipient addresses
)
email.attach('invoice.pdf', pdf_content, 'application/pdf')
#   attach(filename, content, mimetype)
email.send()
```

Set environment variables in a `.env` file (never commit this):

```bash
# .env
EMAIL_HOST_USER=yourapp@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
```

---

### PDF Generation

> 💡 **Analogy:** Generating a PDF is like **printing a web page to paper** — you design the layout with HTML and CSS, then a rendering engine (WeasyPrint) converts it into a portable, pixel-perfect document.

1️⃣ **WHY** — Many applications need to generate invoices, reports, certificates, or receipts as downloadable PDFs. WeasyPrint lets you use your existing HTML/CSS skills instead of learning a low-level PDF library.

2️⃣ **WHEN** — Whenever users need a downloadable or printable document — order invoices, shipping labels, contracts, or any report that must look the same regardless of the viewer's browser.

3️⃣ **HOW**

Install WeasyPrint:

```bash
pip install weasyprint
```

Create an HTML template for the PDF:

```html
<!-- templates/orders/invoice.html -->
<html>
<head>
    <style>
        body { font-family: sans-serif; margin: 2cm; }
        table { width: 100%; border-collapse: collapse; }
        th, td { border: 1px solid #ccc; padding: 8px; text-align: left; }
        .total { font-weight: bold; font-size: 1.2em; }
    </style>
</head>
<body>
    <h1>Invoice #{{ order.id }}</h1>
    <p>Date: {{ order.created|date:"N j, Y" }}</p>
    <p>Customer: {{ order.first_name }} {{ order.last_name }}</p>

    <table>
        <thead>
            <tr><th>Product</th><th>Qty</th><th>Price</th></tr>
        </thead>
        <tbody>
            {% for item in order.items.all %}
            <tr>
                <td>{{ item.product.name }}</td>
                <td>{{ item.quantity }}</td>
                <td>${{ item.get_cost }}</td>
            </tr>
            {% endfor %}
        </tbody>
    </table>
    <p class="total">Total: ${{ order.get_total_cost }}</p>
</body>
</html>
```

Render the PDF in a view and return it as an `HttpResponse`:

```python
# orders/views.py
import weasyprint
from django.template.loader import render_to_string
from django.http import HttpResponse

def generate_invoice_pdf(request, order_id):
    order = get_object_or_404(Order, id=order_id)
    html_string = render_to_string('orders/invoice.html', {'order': order})
    #   Render the HTML template to a string
    pdf = weasyprint.HTML(string=html_string).write_pdf()
    #   Convert the HTML string to a PDF byte string
    response = HttpResponse(pdf, content_type='application/pdf')
    response['Content-Disposition'] = f'filename=invoice_{order.id}.pdf'
    #   Content-Disposition → tells the browser to display inline or download
    return response
```

Send a PDF as an email attachment:

```python
# orders/views.py
from django.core.mail import EmailMessage

def email_invoice(request, order_id):
    order = get_object_or_404(Order, id=order_id)
    html_string = render_to_string('orders/invoice.html', {'order': order})
    pdf = weasyprint.HTML(string=html_string).write_pdf()
    #   Generate the PDF in memory — no temp files needed

    email = EmailMessage(
        subject=f'Invoice #{order.id}',
        body='Please find your invoice attached.',
        from_email='billing@example.com',
        to=[order.email],
    )
    email.attach(f'invoice_{order.id}.pdf', pdf, 'application/pdf')
    #   Attach the PDF bytes with a filename and MIME type
    email.send()
    return redirect('orders:order_detail', order_id=order.id)
```

---

### CSV Export

> 💡 **Analogy:** Exporting to CSV is like copying data from a spreadsheet into a plain text file with commas between columns — it's the universal format that every spreadsheet application, database tool, and data analysis library can read.

1️⃣ **WHY** — CSV exports let administrators and analysts download data for offline processing in Excel, Google Sheets, or pandas. Django makes it easy to generate CSV files on the fly using Python's built-in `csv` module.

2️⃣ **WHEN** — When admins need to export orders, user lists, reports, or any tabular data. A custom admin action is the most convenient approach for exporting directly from the Django admin.

3️⃣ **HOW**

Create a CSV export view:

```python
# orders/views.py
import csv
from django.http import HttpResponse

def export_orders_csv(request):
    response = HttpResponse(content_type='text/csv')
    #   Set the content type so the browser treats it as a file download
    response['Content-Disposition'] = 'attachment; filename="orders.csv"'
    #   attachment → forces download instead of displaying in browser

    writer = csv.writer(response)
    #   Write directly to the HttpResponse object
    writer.writerow(['Order ID', 'Customer', 'Email', 'Total', 'Created'])
    #   Header row

    orders = Order.objects.all()
    for order in orders:
        writer.writerow([
            order.id,
            f'{order.first_name} {order.last_name}',
            order.email,
            order.get_total_cost(),
            order.created.strftime('%Y-%m-%d %H:%M'),
            #   Format the datetime for clean CSV output
        ])
    return response
```

Add a custom admin action to export orders directly from the admin panel:

```python
# orders/admin.py
import csv
from django.http import HttpResponse
from django.contrib import admin
from .models import Order

def export_to_csv(modeladmin, request, queryset):
    """Custom admin action: export selected orders to CSV."""
    opts = modeladmin.model._meta
    #   _meta → access model metadata (app label, field names)
    response = HttpResponse(content_type='text/csv')
    response['Content-Disposition'] = f'attachment; filename="{opts.verbose_name_plural}.csv"'

    writer = csv.writer(response)
    fields = [f for f in opts.get_fields() if not f.many_to_many and not f.one_to_many]
    #   Exclude reverse relations and many-to-many fields
    writer.writerow([f.verbose_name for f in fields])
    #   Header row using human-readable field names

    for obj in queryset:
        row = [getattr(obj, f.name) for f in fields]
        writer.writerow(row)
    return response

export_to_csv.short_description = 'Export to CSV'
#   Label shown in the admin action dropdown

@admin.register(Order)
class OrderAdmin(admin.ModelAdmin):
    list_display = ['id', 'first_name', 'last_name', 'email', 'paid', 'created']
    list_filter = ['paid', 'created']
    actions = [export_to_csv]
    #   Register the custom action so it appears in the admin dropdown
```

Select orders in the admin, choose "Export to CSV" from the action dropdown, and click "Go" to download.

---

### Payment Integration (Stripe)

> 💡 **Analogy:** Stripe Checkout is like a **valet parking service** — instead of building your own payment form and handling card numbers yourself, you hand the customer off to Stripe's secure hosted page. When payment is done, Stripe sends you a receipt (webhook) confirming what happened.

1️⃣ **WHY** — Handling credit card data directly exposes you to PCI compliance requirements and security risks. Stripe Checkout offloads the entire payment form to Stripe's servers, so card numbers never touch your backend.

2️⃣ **WHEN** — Any e-commerce application that needs to accept payments. Stripe supports one-time payments, subscriptions, and multiple currencies.

3️⃣ **HOW**

Install the Stripe Python library:

```bash
pip install stripe
```

Configure Stripe keys in `settings.py`:

```python
# settings.py
import os

STRIPE_PUBLISHABLE_KEY = os.environ.get('STRIPE_PUBLISHABLE_KEY')
#   Public key — safe to expose in templates
STRIPE_SECRET_KEY = os.environ.get('STRIPE_SECRET_KEY')
#   Secret key — never expose in client-side code
STRIPE_WEBHOOK_SECRET = os.environ.get('STRIPE_WEBHOOK_SECRET')
#   Used to verify that webhooks really come from Stripe
```

Create a checkout session:

```python
# payment/views.py
import stripe
from django.conf import settings
from django.shortcuts import redirect, get_object_or_404
from orders.models import Order

stripe.api_key = settings.STRIPE_SECRET_KEY

def create_checkout_session(request, order_id):
    order = get_object_or_404(Order, id=order_id)
    session = stripe.checkout.Session.create(
        payment_method_types=['card'],
        #   Accept credit/debit cards
        line_items=[{
            'price_data': {
                'currency': 'usd',
                'unit_amount': int(order.get_total_cost() * 100),
                #   Stripe uses cents — multiply dollars by 100
                'product_data': {
                    'name': f'Order #{order.id}',
                },
            },
            'quantity': 1,
        }],
        mode='payment',
        #   mode='payment' for one-time charges
        success_url=request.build_absolute_uri(f'/payment/success/{order.id}/'),
        cancel_url=request.build_absolute_uri(f'/payment/cancelled/{order.id}/'),
        client_reference_id=str(order.id),
        #   Attach order ID so the webhook can link payment to order
    )
    return redirect(session.url, code=303)
    #   303 redirect to Stripe's hosted checkout page
```

Handle success and cancellation:

```python
# payment/views.py
def payment_success(request, order_id):
    order = get_object_or_404(Order, id=order_id)
    return render(request, 'payment/success.html', {'order': order})

def payment_cancelled(request, order_id):
    order = get_object_or_404(Order, id=order_id)
    return render(request, 'payment/cancelled.html', {'order': order})
```

Create a webhook endpoint to receive payment notifications:

```python
# payment/webhooks.py
import stripe
from django.conf import settings
from django.http import HttpResponse
from django.views.decorators.csrf import csrf_exempt
from orders.models import Order

@csrf_exempt
#   Stripe sends POST requests without a CSRF token
def stripe_webhook(request):
    payload = request.body
    sig_header = request.META.get('HTTP_STRIPE_SIGNATURE')
    #   Stripe includes a signature header for verification

    try:
        event = stripe.Webhook.construct_event(
            payload, sig_header, settings.STRIPE_WEBHOOK_SECRET
        )
        #   Verify the webhook signature to prevent spoofing
    except (ValueError, stripe.error.SignatureVerificationError):
        return HttpResponse(status=400)
        #   Invalid payload or signature — reject the request

    if event['type'] == 'checkout.session.completed':
        session = event['data']['object']
        order_id = session.get('client_reference_id')
        #   Retrieve the order ID we attached earlier
        order = Order.objects.get(id=order_id)
        order.paid = True
        order.save()
        #   Mark the order as paid

    return HttpResponse(status=200)
    #   Always return 200 so Stripe doesn't retry
```

Register webhook URL:

```python
# payment/urls.py
urlpatterns = [
    path('checkout/<int:order_id>/', create_checkout_session, name='checkout'),
    path('success/<int:order_id>/', payment_success, name='success'),
    path('cancelled/<int:order_id>/', payment_cancelled, name='cancelled'),
    path('webhook/', stripe_webhook, name='stripe_webhook'),
]
```

Test with Stripe's test card number: `4242 4242 4242 4242`, any future expiry, any 3-digit CVC.

---

### Tagging with django-taggit

> 💡 **Analogy:** Tags are like **sticky notes on a filing cabinet** — instead of organizing files into rigid folder hierarchies, you stick labels on each file so it can belong to multiple categories at once. Searching by tag pulls all matching files instantly.

1️⃣ **WHY** — Tags provide a flexible, user-friendly way to categorize content without rigid hierarchies. `django-taggit` handles the many-to-many relationship, tag normalization, and querying so you don't have to build it yourself.

2️⃣ **WHEN** — Blogs (tag posts by topic), e-commerce (tag products by feature), knowledge bases, or any model where items belong to multiple overlapping categories.

3️⃣ **HOW**

Install django-taggit:

```bash
pip install django-taggit
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'taggit',
    #   Provides Tag and TaggedItem models automatically
]
```

Add tags to your model:

```python
# blog/models.py
from taggit.managers import TaggableManager

class Post(models.Model):
    title = models.CharField(max_length=250)
    body = models.TextField()
    status = models.CharField(max_length=10, default='draft')
    tags = TaggableManager()
    #   Adds a many-to-many relationship to taggit's Tag model
    ...
```

Run migrations:

```bash
python manage.py makemigrations && python manage.py migrate
```

Work with tags in the shell or views:

```python
# Adding and removing tags
post = Post.objects.get(id=1)
post.tags.add('django', 'python', 'web')
#   Add multiple tags at once
post.tags.remove('web')
#   Remove a single tag
post.tags.all()
#   <QuerySet [<Tag: django>, <Tag: python>]>
```

Filter posts by tag:

```python
# blog/views.py
from taggit.models import Tag

def post_list(request, tag_slug=None):
    posts = Post.objects.filter(status='published')
    tag = None
    if tag_slug:
        tag = get_object_or_404(Tag, slug=tag_slug)
        posts = posts.filter(tags__in=[tag])
        #   Filter to posts that have this specific tag
    return render(request, 'blog/list.html', {
        'posts': posts, 'tag': tag,
    })
```

Display tags in templates:

```html
<!-- templates/blog/post_detail.html -->
<p>Tags:
  {% for tag in post.tags.all %}
    <a href="{% url 'blog:post_list_by_tag' tag.slug %}">
      {{ tag.name }}
    </a>
    {% if not forloop.last %}, {% endif %}
    <!-- Comma-separate tags, skip comma after last one -->
  {% endfor %}
</p>
```

Retrieve similar posts by shared tags:

```python
# blog/views.py
from django.db.models import Count

def post_detail(request, post_id):
    post = get_object_or_404(Post, id=post_id, status='published')
    post_tags_ids = post.tags.values_list('id', flat=True)
    #   Get IDs of all tags on this post
    similar_posts = Post.objects.filter(
        status='published', tags__in=post_tags_ids
    ).exclude(id=post.id).annotate(
        same_tags=Count('tags')
        #   Count how many tags each post shares with the current post
    ).order_by('-same_tags', '-publish_date')[:4]
    #   Most similar posts first, limited to 4

    return render(request, 'blog/detail.html', {
        'post': post,
        'similar_posts': similar_posts,
    })
```

---

### Image Handling and Thumbnails

> 💡 **Analogy:** Uploading a full-resolution photo and displaying it as a tiny avatar is like **shipping a grand piano when you only need a keyboard** — thumbnails resize images to the exact dimensions needed, saving bandwidth and speeding up page loads.

1️⃣ **WHY** — User-uploaded images are often much larger than needed for display. Serving full-size images wastes bandwidth and slows pages. Thumbnail libraries generate resized versions on the fly or on first access.

2️⃣ **WHEN** — Any application with user-uploaded images — profile photos, product images, gallery sites. Use `ImageField` for uploads and `easy-thumbnails` for automatic resizing.

3️⃣ **HOW**

Install Pillow (required for `ImageField`) and easy-thumbnails:

```bash
pip install Pillow easy-thumbnails
```

```python
# settings.py
INSTALLED_APPS = [
    ...
    'easy_thumbnails',
    #   Provides template tags and management commands for thumbnailing
]

MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
#   Directory where uploaded files are stored on disk
```

Add an `ImageField` to your model:

```python
# shop/models.py
class Product(models.Model):
    name = models.CharField(max_length=200)
    image = models.ImageField(upload_to='products/%Y/%m/%d', blank=True)
    #   upload_to → subdirectory under MEDIA_ROOT, organized by date
    #   blank=True → image is optional
    ...
```

Run migrations:

```bash
python manage.py makemigrations && python manage.py migrate
```

Use easy-thumbnails in templates:

```html
<!-- templates/shop/product_detail.html -->
{% load thumbnail %}

{% if product.image %}
  <img src="{% thumbnail product.image 300x300 crop %}"
       alt="{{ product.name }}">
  <!-- 300x300 → target dimensions in pixels -->
  <!-- crop → crop to exact size instead of stretching -->
{% else %}
  <img src="{% static 'img/no-image.png' %}" alt="No image available">
{% endif %}
```

Configure thumbnail options in settings:

```python
# settings.py
THUMBNAIL_ALIASES = {
    '': {
        'small': {'size': (100, 100), 'crop': True},
        #   Named alias — use as {% thumbnail image "small" %}
        'medium': {'size': (300, 300), 'crop': True},
        'large': {'size': (600, 600), 'crop': False},
        #   crop=False → resize preserving aspect ratio
    },
}
```

```html
<!-- Using named aliases -->
{% load thumbnail %}
<img src="{% thumbnail product.image 'medium' %}" alt="{{ product.name }}">
```

Clean up stale thumbnails periodically:

```bash
python manage.py thumbnail_cleanup
#   Removes thumbnails for source images that no longer exist
```

---

### Django Channels and WebSockets

> 💡 **Analogy:** Traditional Django (WSGI) is like a **post office** — the client sends a request and waits for a response. Django Channels (ASGI) upgrades it to a **telephone line** — both sides can talk at any time, enabling real-time features like chat, notifications, and live updates.

1️⃣ **WHY** — HTTP is request-response: the server cannot push updates to the client. WebSockets maintain a persistent bidirectional connection, enabling real-time features without polling. Django Channels extends Django to handle WebSockets, long-polling, and other async protocols.

2️⃣ **WHEN** — Chat applications, live notifications, collaborative editing, real-time dashboards, multiplayer games — any feature where the server needs to push data to the client instantly.

3️⃣ **HOW**

Install Channels and Daphne (the ASGI server):

```bash
pip install channels daphne channels-redis
```

```python
# settings.py
INSTALLED_APPS = [
    'daphne',
    #   Must be listed before django.contrib.staticfiles
    ...
]

ASGI_APPLICATION = 'mysite.asgi.application'
#   Points to the ASGI application entry point

CHANNEL_LAYERS = {
    'default': {
        'BACKEND': 'channels_redis.core.RedisChannelLayer',
        'CONFIG': {
            'hosts': [('127.0.0.1', 6379)],
            #   Redis server for channel layer — enables cross-process messaging
        },
    },
}
```

Configure the ASGI application:

```python
# mysite/asgi.py
import os
from channels.routing import ProtocolTypeRouter, URLRouter
from channels.auth import AuthMiddlewareStack
from django.core.asgi import get_asgi_application
import chat.routing

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')

application = ProtocolTypeRouter({
    'http': get_asgi_application(),
    #   Handle normal HTTP requests
    'websocket': AuthMiddlewareStack(
        URLRouter(chat.routing.websocket_urlpatterns)
    ),
    #   Handle WebSocket connections with Django authentication
})
```

Define WebSocket URL routing:

```python
# chat/routing.py
from django.urls import re_path
from . import consumers

websocket_urlpatterns = [
    re_path(r'ws/chat/(?P<room_name>\w+)/$', consumers.ChatConsumer.as_asgi()),
    #   WebSocket URL pattern — matches /ws/chat/lobby/ etc.
]
```

Write a consumer (WebSocket handler):

```python
# chat/consumers.py
import json
from channels.generic.websocket import AsyncWebsocketConsumer
from channels.db import database_sync_to_async
from .models import Message

class ChatConsumer(AsyncWebsocketConsumer):
    async def connect(self):
        self.room_name = self.scope['url_route']['kwargs']['room_name']
        #   Extract room name from the URL
        self.room_group_name = f'chat_{self.room_name}'

        await self.channel_layer.group_add(
            self.room_group_name, self.channel_name
        )
        #   Join the room group — all members receive broadcasts
        await self.accept()
        #   Accept the WebSocket connection

    async def disconnect(self, close_code):
        await self.channel_layer.group_discard(
            self.room_group_name, self.channel_name
        )
        #   Leave the room group on disconnect

    async def receive(self, text_data):
        data = json.loads(text_data)
        message = data['message']
        username = self.scope['user'].username
        #   Access the authenticated user from the scope

        await self.save_message(username, self.room_name, message)
        #   Persist the message to the database

        await self.channel_layer.group_send(
            self.room_group_name,
            {
                'type': 'chat_message',
                #   type → maps to the chat_message method below
                'message': message,
                'username': username,
            }
        )

    async def chat_message(self, event):
        """Broadcast message to all group members."""
        await self.send(text_data=json.dumps({
            'message': event['message'],
            'username': event['username'],
        }))

    @database_sync_to_async
    def save_message(self, username, room, message):
        """Save chat message to the database."""
        Message.objects.create(
            user=self.scope['user'],
            room=room,
            content=message,
        )
```

WebSocket client in JavaScript:

```javascript
// static/js/chat.js
const roomName = JSON.parse(
    document.getElementById('room-name').textContent
);
const chatSocket = new WebSocket(
    'ws://' + window.location.host + '/ws/chat/' + roomName + '/'
);
//   Open a WebSocket connection to the server

chatSocket.onmessage = function(e) {
    const data = JSON.parse(e.data);
    //   Parse the incoming JSON message
    const chatLog = document.getElementById('chat-log');
    chatLog.innerHTML += '<p><b>' + data.username + ':</b> ' + data.message + '</p>';
};

document.getElementById('chat-form').onsubmit = function(e) {
    e.preventDefault();
    const input = document.getElementById('chat-input');
    chatSocket.send(JSON.stringify({
        'message': input.value
    }));
    //   Send the message as JSON over the WebSocket
    input.value = '';
};
```

---

### Building a Follow System

> 💡 **Analogy:** A follow system is like **subscribing to a magazine** — you choose whose content you want to see in your feed. The intermediate `Contact` model is the subscription record that tracks who follows whom and when.

1️⃣ **WHY** — Social features like following, activity streams, and personalized feeds require tracking relationships between users. A many-to-many relationship with an intermediate model gives you full control over metadata (e.g., when the follow happened).

2️⃣ **WHEN** — Social networks, content platforms, any application where users want to follow other users and see their activity.

3️⃣ **HOW**

Create an intermediate model for the follow relationship:

```python
# accounts/models.py
from django.db import models
from django.contrib.auth.models import User

class Contact(models.Model):
    user_from = models.ForeignKey(
        User, related_name='rel_from_set', on_delete=models.CASCADE
    )
    #   The user who initiates the follow
    user_to = models.ForeignKey(
        User, related_name='rel_to_set', on_delete=models.CASCADE
    )
    #   The user being followed
    created = models.DateTimeField(auto_now_add=True)
    #   When the follow happened

    class Meta:
        indexes = [models.Index(fields=['-created'])]
        ordering = ['-created']
        constraints = [
            models.UniqueConstraint(
                fields=['user_from', 'user_to'],
                name='unique_follow'
            )
            #   Prevent duplicate follows
        ]

    def __str__(self):
        return f'{self.user_from} follows {self.user_to}'
```

Add a convenience accessor to the `User` model:

```python
# accounts/models.py (continued)
User.add_to_class(
    'following',
    models.ManyToManyField(
        'self', through=Contact, related_name='followers',
        symmetrical=False
    )
    #   symmetrical=False → following someone doesn't mean they follow you back
)
```

Create follow/unfollow views:

```python
# accounts/views.py
from django.contrib.auth.decorators import login_required
from django.http import JsonResponse
from django.shortcuts import get_object_or_404
from django.contrib.auth.models import User
from .models import Contact

@login_required
def user_follow(request):
    if request.method == 'POST':
        user_id = request.POST.get('id')
        action = request.POST.get('action')
        #   action is either 'follow' or 'unfollow'
        if user_id and action:
            user = get_object_or_404(User, id=user_id)
            if action == 'follow':
                Contact.objects.get_or_create(
                    user_from=request.user, user_to=user
                )
                #   get_or_create → avoids duplicate follow records
            else:
                Contact.objects.filter(
                    user_from=request.user, user_to=user
                ).delete()
            return JsonResponse({'status': 'ok'})
    return JsonResponse({'status': 'error'})
```

List followers and following:

```python
# accounts/views.py
@login_required
def user_detail(request, username):
    user = get_object_or_404(User, username=username, is_active=True)
    followers = user.followers.all()
    #   Users who follow this user (via related_name='followers')
    following = user.following.all()
    #   Users this user follows
    is_following = Contact.objects.filter(
        user_from=request.user, user_to=user
    ).exists()
    #   Check if the current user already follows this user

    return render(request, 'accounts/user_detail.html', {
        'user': user,
        'followers': followers,
        'following': following,
        'is_following': is_following,
    })
```

Display in templates:

```html
<!-- templates/accounts/user_detail.html -->
<h2>{{ user.username }}</h2>
<p>{{ followers.count }} follower{{ followers.count|pluralize }}</p>
<p>Following {{ following.count }} user{{ following.count|pluralize }}</p>

{% if user != request.user %}
  <button id="follow-btn"
          data-id="{{ user.id }}"
          data-action="{% if is_following %}unfollow{% else %}follow{% endif %}">
    {% if is_following %}Unfollow{% else %}Follow{% endif %}
  </button>
{% endif %}
```

---

### Asynchronous JavaScript with Django

> 💡 **Analogy:** Traditional form submissions are like **sending a letter and waiting for a reply** — the entire page reloads. AJAX requests are like **texting** — you send a message and the reply appears instantly on the same screen without interrupting what you're doing.

1️⃣ **WHY** — Full page reloads feel sluggish and disrupt the user experience. Asynchronous JavaScript lets you update parts of the page without reloading, creating a smoother, app-like feel. Actions like liking a post, following a user, or loading more content should happen seamlessly.

2️⃣ **WHEN** — Like/unlike buttons, follow/unfollow actions, infinite scroll pagination, live search, any interaction where a full page reload is unnecessary.

3️⃣ **HOW**

**Include the CSRF token for JavaScript requests:**

```html
<!-- templates/base.html -->
{% csrf_token %}
<script>
    //   Read the CSRF token from the hidden input
    const csrfToken = document.querySelector('[name=csrfmiddlewaretoken]').value;
</script>
```

**Like/unlike button without page refresh:**

```python
# blog/views.py
from django.http import JsonResponse
from django.contrib.auth.decorators import login_required

@login_required
def post_like(request):
    if request.method == 'POST':
        post_id = request.POST.get('id')
        action = request.POST.get('action')
        #   'like' or 'unlike'
        post = get_object_or_404(Post, id=post_id)
        if action == 'like':
            post.likes.add(request.user)
            #   Add user to the many-to-many likes field
        else:
            post.likes.remove(request.user)
        return JsonResponse({
            'status': 'ok',
            'total_likes': post.likes.count(),
            #   Return updated count so JS can refresh the display
        })
    return JsonResponse({'status': 'error'})
```

```javascript
// static/js/like.js
document.addEventListener('DOMContentLoaded', function() {
    //   Run after the DOM is fully loaded
    const likeButtons = document.querySelectorAll('.like-btn');

    likeButtons.forEach(function(btn) {
        btn.addEventListener('click', function(e) {
            e.preventDefault();
            const postId = this.dataset.id;
            const action = this.dataset.action;
            //   Read data-id and data-action attributes from the button

            fetch('/blog/like/', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/x-www-form-urlencoded',
                    'X-CSRFToken': csrfToken,
                    //   Include CSRF token in the request header
                },
                body: `id=${postId}&action=${action}`,
            })
            .then(response => response.json())
            .then(data => {
                if (data.status === 'ok') {
                    //   Toggle the button text and action
                    this.dataset.action = action === 'like' ? 'unlike' : 'like';
                    this.textContent = action === 'like' ? 'Unlike' : 'Like';
                    //   Update the like count on the page
                    document.getElementById(`likes-${postId}`).textContent = data.total_likes;
                }
            });
        });
    });
});
```

**Infinite scroll pagination:**

```python
# blog/views.py
from django.core.paginator import Paginator, EmptyPage

def post_list_ajax(request):
    posts = Post.objects.filter(status='published')
    paginator = Paginator(posts, 10)
    #   10 posts per page
    page = request.GET.get('page', 1)
    try:
        posts = paginator.page(page)
    except EmptyPage:
        if request.headers.get('X-Requested-With') == 'XMLHttpRequest':
            return HttpResponse('')
            #   Return empty response when AJAX reaches the last page
        posts = paginator.page(paginator.num_pages)
    if request.headers.get('X-Requested-With') == 'XMLHttpRequest':
        return render(request, 'blog/post_list_partial.html', {'posts': posts})
        #   Return only the partial template for AJAX requests
    return render(request, 'blog/post_list.html', {'posts': posts})
```

```javascript
// static/js/infinite_scroll.js
let page = 1;
let loading = false;

window.addEventListener('scroll', function() {
    //   Detect when user scrolls near the bottom of the page
    if (loading) return;
    const scrollHeight = document.documentElement.scrollHeight;
    const scrollTop = document.documentElement.scrollTop;
    const clientHeight = document.documentElement.clientHeight;

    if (scrollTop + clientHeight >= scrollHeight - 200) {
        //   200px threshold — start loading before hitting the very bottom
        loading = true;
        page++;
        fetch(`?page=${page}`, {
            headers: { 'X-Requested-With': 'XMLHttpRequest' },
            //   Signal to Django that this is an AJAX request
        })
        .then(response => response.text())
        .then(html => {
            if (html.trim()) {
                document.getElementById('post-list').insertAdjacentHTML('beforeend', html);
                //   Append new posts to the existing list
            }
            loading = false;
        });
    }
});
```

---

### Coupon System

> 💡 **Analogy:** A coupon system is like a **bouncer with a guest list** — the coupon code is checked against the list (database), verified for validity dates and active status, and only then does the customer get the discount applied to their total.

1️⃣ **WHY** — Coupons drive sales, reward loyal customers, and support marketing campaigns. A database-backed coupon system lets you control validity periods, usage limits, and discount amounts dynamically.

2️⃣ **WHEN** — E-commerce sites, SaaS applications offering trial discounts, any platform where promotional pricing is a business requirement.

3️⃣ **HOW**

Create the coupon model:

```python
# coupons/models.py
from django.db import models
from django.core.validators import MinValueValidator, MaxValueValidator

class Coupon(models.Model):
    code = models.CharField(max_length=50, unique=True)
    #   The code customers enter (e.g., SAVE20)
    valid_from = models.DateTimeField()
    #   Coupon becomes active at this datetime
    valid_to = models.DateTimeField()
    #   Coupon expires after this datetime
    discount = models.IntegerField(
        validators=[MinValueValidator(0), MaxValueValidator(100)]
    )
    #   Percentage discount (0-100)
    active = models.BooleanField()
    #   Admin can manually enable/disable coupons

    def __str__(self):
        return self.code
```

Create a form for applying coupons:

```python
# coupons/forms.py
from django import forms

class CouponApplyForm(forms.Form):
    code = forms.CharField(max_length=50)
    #   A single text input for the coupon code
```

Validate and apply the coupon:

```python
# coupons/views.py
from django.shortcuts import redirect
from django.utils import timezone
from .models import Coupon
from .forms import CouponApplyForm

def coupon_apply(request):
    if request.method == 'POST':
        form = CouponApplyForm(request.POST)
        if form.is_valid():
            code = form.cleaned_data['code']
            now = timezone.now()
            try:
                coupon = Coupon.objects.get(
                    code__iexact=code,
                    #   Case-insensitive match
                    valid_from__lte=now,
                    #   Must have started
                    valid_to__gte=now,
                    #   Must not have expired
                    active=True,
                    #   Must be active
                )
                request.session['coupon_id'] = coupon.id
                #   Store coupon in the session for use during checkout
            except Coupon.DoesNotExist:
                request.session['coupon_id'] = None
                #   Invalid code — clear any previous coupon
            return redirect('cart:cart_detail')
```

Apply the discount in the cart:

```python
# cart/cart.py
from decimal import Decimal
from coupons.models import Coupon

class Cart:
    def __init__(self, request):
        self.session = request.session
        self.coupon_id = self.session.get('coupon_id')

    @property
    def coupon(self):
        if self.coupon_id:
            try:
                return Coupon.objects.get(id=self.coupon_id)
            except Coupon.DoesNotExist:
                pass
        return None

    def get_discount(self):
        if self.coupon:
            return (self.coupon.discount / Decimal(100)) * self.get_total_price()
            #   Calculate the discount amount from the percentage
        return Decimal(0)

    def get_total_price_after_discount(self):
        return self.get_total_price() - self.get_discount()
        #   Subtract discount from the original total
```

Store the coupon on the order at checkout:

```python
# orders/models.py
class Order(models.Model):
    ...
    coupon = models.ForeignKey(
        'coupons.Coupon', related_name='orders',
        null=True, blank=True, on_delete=models.SET_NULL
    )
    #   SET_NULL → keep the order even if the coupon is deleted
    discount = models.IntegerField(default=0,
        validators=[MinValueValidator(0), MaxValueValidator(100)]
    )
    #   Snapshot the discount percentage at time of order

    def get_total_cost(self):
        total = sum(item.get_cost() for item in self.items.all())
        return total - total * (self.discount / Decimal(100))
```

---

### Recommendation Engine

> 💡 **Analogy:** A recommendation engine is like a **bookstore clerk who remembers what other customers bought** — "People who bought X also bought Y." By tracking purchase patterns, you can suggest products that are statistically likely to interest the current buyer.

1️⃣ **WHY** — Product recommendations increase average order value and improve user engagement. A simple "frequently bought together" engine based on co-purchase data is effective and easy to implement using Redis sorted sets.

2️⃣ **WHEN** — E-commerce sites, content platforms (related articles), streaming services (related videos). Even a basic recommendation engine outperforms showing random items.

3️⃣ **HOW**

Install Redis:

```bash
pip install redis
```

Build a recommender class using Redis sorted sets:

```python
# shop/recommender.py
import redis
from django.conf import settings
from .models import Product

r = redis.Redis(
    host=settings.REDIS_HOST,
    port=settings.REDIS_PORT,
    db=settings.REDIS_DB,
)
#   Connect to Redis — configure host/port/db in settings.py

class Recommender:
    def get_product_key(self, id):
        return f'product:{id}:purchased_with'
        #   Redis key pattern: each product has a sorted set of co-purchases

    def products_bought(self, products):
        """Record that these products were bought together."""
        product_ids = [p.id for p in products]
        for product_id in product_ids:
            for with_id in product_ids:
                if product_id != with_id:
                    r.zincrby(
                        self.get_product_key(product_id),
                        1,
                        with_id,
                    )
                    #   zincrby → increment the score of with_id by 1
                    #   Higher score = more frequently bought together

    def suggest_products_for(self, products, max_results=6):
        """Suggest products commonly bought with the given products."""
        product_ids = [p.id for p in products]
        if len(product_ids) == 1:
            suggestions = r.zrange(
                self.get_product_key(product_ids[0]),
                0, -1, desc=True,
            )
            #   Get all co-purchased product IDs sorted by score descending
        else:
            flat_ids = ''.join([str(id) for id in product_ids])
            tmp_key = f'tmp:{flat_ids}'
            #   Temporary key for combining multiple products
            keys = [self.get_product_key(id) for id in product_ids]
            r.zunionstore(tmp_key, keys)
            #   Union all sorted sets — scores are summed
            r.zrem(tmp_key, *product_ids)
            #   Remove the input products from suggestions
            suggestions = r.zrange(tmp_key, 0, -1, desc=True)[:max_results]
            r.delete(tmp_key)
            #   Clean up the temporary key

        suggested_product_ids = [int(id) for id in suggestions]
        suggested_products = list(
            Product.objects.filter(id__in=suggested_product_ids)
        )
        #   Fetch Product objects from MySQL

        suggested_products.sort(
            key=lambda x: suggested_product_ids.index(x.id)
        )
        #   Preserve the Redis score ordering
        return suggested_products
```

Record purchases after a successful order:

```python
# orders/views.py
from shop.recommender import Recommender

def order_created(request, order):
    r = Recommender()
    products = [item.product for item in order.items.all()]
    r.products_bought(products)
    #   Store co-purchase relationships for all products in this order
```

Display recommendations in a product detail view:

```python
# shop/views.py
from .recommender import Recommender

def product_detail(request, id, slug):
    product = get_object_or_404(Product, id=id, slug=slug, available=True)
    r = Recommender()
    recommended = r.suggest_products_for([product], max_results=4)
    #   Get up to 4 products frequently bought with this one

    return render(request, 'shop/product_detail.html', {
        'product': product,
        'recommended_products': recommended,
    })
```

```html
<!-- templates/shop/product_detail.html -->
{% if recommended_products %}
<h3>People who bought this also bought</h3>
<div class="recommendations">
    {% for p in recommended_products %}
    <div class="product-card">
        <a href="{{ p.get_absolute_url }}">{{ p.name }}</a>
        <p>${{ p.price }}</p>
    </div>
    {% endfor %}
</div>
{% endif %}
```

---

### Extending the Admin Site

> 💡 **Analogy:** Django's admin is like a **pre-built office** — it comes with desks, chairs, and filing cabinets. Extending the admin is like **adding a custom conference room** — you add specialized views, reports, and workflows that go beyond basic CRUD operations.

1️⃣ **WHY** — The default admin handles CRUD well, but real-world applications need custom dashboards, batch operations, report views, and specialized workflows. Django lets you add custom views, URLs, templates, and actions to the admin without building a separate interface.

2️⃣ **WHEN** — When admin users need to perform operations beyond simple add/edit/delete — generating reports, triggering batch processes, viewing dashboards, or accessing custom tools.

3️⃣ **HOW**

**Add custom admin actions for batch operations:**

```python
# orders/admin.py
from django.contrib import admin
from .models import Order

def mark_as_paid(modeladmin, request, queryset):
    """Batch action: mark selected orders as paid."""
    queryset.update(paid=True)
    #   Single SQL UPDATE for all selected rows — efficient
mark_as_paid.short_description = 'Mark selected orders as paid'

def mark_as_shipped(modeladmin, request, queryset):
    """Batch action: mark selected orders as shipped."""
    updated = queryset.update(status='shipped')
    modeladmin.message_user(request, f'{updated} orders marked as shipped.')
    #   message_user → show a success message in the admin
mark_as_shipped.short_description = 'Mark selected orders as shipped'

@admin.register(Order)
class OrderAdmin(admin.ModelAdmin):
    list_display = ['id', 'first_name', 'last_name', 'paid', 'status', 'created']
    list_filter = ['paid', 'status', 'created']
    actions = [mark_as_paid, mark_as_shipped]
    #   Both actions appear in the action dropdown
```

**Add custom URLs and views to the admin:**

```python
# orders/admin.py
from django.urls import path
from django.template.response import TemplateResponse
from django.db.models import Count, Sum

@admin.register(Order)
class OrderAdmin(admin.ModelAdmin):
    ...

    def get_urls(self):
        urls = super().get_urls()
        custom_urls = [
            path('dashboard/', self.admin_site.admin_view(self.dashboard_view),
                 name='orders_dashboard'),
            #   admin_view() wraps the view with permission checks and caching
        ]
        return custom_urls + urls
        #   Custom URLs must come before default ones to avoid being overridden

    def dashboard_view(self, request):
        """Custom admin view: order dashboard with statistics."""
        summary = Order.objects.aggregate(
            total_orders=Count('id'),
            total_revenue=Sum('total'),
            paid_orders=Count('id', filter=models.Q(paid=True)),
            #   Aggregate stats in a single query
        )
        context = {
            **self.admin_site.each_context(request),
            #   Include admin site context (site_title, has_permission, etc.)
            'summary': summary,
            'title': 'Order Dashboard',
        }
        return TemplateResponse(request, 'admin/orders/dashboard.html', context)
```

**Create a custom admin template:**

```html
<!-- templates/admin/orders/dashboard.html -->
{% extends "admin/base_site.html" %}
{% load i18n %}

{% block title %}Order Dashboard{% endblock %}

{% block content %}
<h2>Order Dashboard</h2>
<div class="dashboard-stats">
    <div class="stat-card">
        <h3>Total Orders</h3>
        <p>{{ summary.total_orders }}</p>
    </div>
    <div class="stat-card">
        <h3>Total Revenue</h3>
        <p>${{ summary.total_revenue|default:"0.00" }}</p>
    </div>
    <div class="stat-card">
        <h3>Paid Orders</h3>
        <p>{{ summary.paid_orders }}</p>
    </div>
</div>
{% endblock %}
```

**Override default admin templates:**

```
templates/
  admin/
    base_site.html          ← Override the admin header/branding
    orders/
      dashboard.html        ← Custom view template
      change_list.html      ← Override the order list page
```

```html
<!-- templates/admin/base_site.html -->
{% extends "admin/base.html" %}

{% block title %}My Store Admin | {{ title }}{% endblock %}

{% block branding %}
<h1 id="site-name">
    <a href="{% url 'admin:index' %}">My Store Administration</a>
    <!-- Custom branding replaces the default "Django administration" text -->
</h1>
{% endblock %}
```

Add a link to the custom dashboard on the admin index page:

```python
# orders/admin.py (inside OrderAdmin)
def changelist_view(self, request, extra_context=None):
    extra_context = extra_context or {}
    extra_context['dashboard_url'] = 'admin:orders_dashboard'
    #   Pass the dashboard URL name to the template context
    return super().changelist_view(request, extra_context=extra_context)
```

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
# Run the block that matches your operating system:

# Linux / macOS
export DJANGO_SECRET_KEY='your-very-long-random-secret-key'
export DB_PASSWORD='your-db-password'
export DJANGO_SETTINGS_MODULE='mysite.settings'

# Windows (Command Prompt) — run these instead of the export lines above:
# set DJANGO_SECRET_KEY=your-very-long-random-secret-key
# set DB_PASSWORD=your-db-password
# set DJANGO_SETTINGS_MODULE=mysite.settings

# Windows (PowerShell) — run these instead of the export lines above:
# $env:DJANGO_SECRET_KEY = 'your-very-long-random-secret-key'
# $env:DB_PASSWORD = 'your-db-password'
# $env:DJANGO_SETTINGS_MODULE = 'mysite.settings'

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


### Managing Settings for Multiple Environments

> 💡 **Analogy:** Think of your settings like a wardrobe — you have a **base layer** everyone wears (base.py), a **casual outfit** for home (local.py), and a **formal suit** for work (production.py). You pick the right outfit for the occasion using an environment variable.

1️⃣ **WHY** — A single `settings.py` file forces you to toggle `DEBUG`, database credentials, and secret keys manually every time you switch between development and production. Splitting settings into separate files per environment eliminates human error and keeps secrets out of version control.

2️⃣ **WHEN** — As soon as your project moves beyond local development — any time you have more than one deployment target (local machine, staging server, production server).

3️⃣ **HOW**

Create a settings package that replaces the default `settings.py` module:

```bash
# Convert the single settings.py into a package
mkdir mysite/settings
mv mysite/settings.py mysite/settings/base.py
touch mysite/settings/__init__.py
#   __init__.py → makes the directory a Python package
#   base.py     → shared settings inherited by all environments
```

```python
# mysite/settings/base.py — shared settings for ALL environments
import os
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent.parent
#   parent.parent.parent → up from settings/ → mysite/ → project root

SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY', 'change-me-in-production')
#   os.environ.get() → reads from environment variable
#   Never hard-code the real secret in source control

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Your apps
    'blog.apps.BlogConfig',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'mysite.urls'
WSGI_APPLICATION = 'mysite.wsgi.application'

# Database defaults — overridden per environment
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': os.environ.get('DB_NAME', 'mydb'),
        'USER': os.environ.get('DB_USER', 'myuser'),
        'PASSWORD': os.environ.get('DB_PASSWORD', ''),
        'HOST': os.environ.get('DB_HOST', '127.0.0.1'),
        'PORT': os.environ.get('DB_PORT', '3306'),
        'OPTIONS': {
            'init_command': "SET sql_mode='STRICT_TRANS_TABLES'",
            'charset': 'utf8mb4',
            #   charset=utf8mb4 → full Unicode support in MySQL
        },
    }
}

STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

```python
# mysite/settings/local.py — development overrides
from .base import *
#   import * → inherit every setting from base.py

DEBUG = True
#   True → shows detailed error pages during development

ALLOWED_HOSTS = ['localhost', '127.0.0.1']
#   Only accept requests from local machine

# Use a local MySQL instance with relaxed credentials
DATABASES['default']['NAME'] = 'mydb_dev'
DATABASES['default']['HOST'] = '127.0.0.1'

# Optional: Django Debug Toolbar for profiling queries
INSTALLED_APPS += ['debug_toolbar']
#   += → appends to the list inherited from base.py
MIDDLEWARE.insert(0, 'debug_toolbar.middleware.DebugToolbarMiddleware')
INTERNAL_IPS = ['127.0.0.1']
```

```python
# mysite/settings/production.py — production overrides
from .base import *
#   import * → inherit every setting from base.py

DEBUG = False
#   False → never expose stack traces in production

ALLOWED_HOSTS = os.environ.get('ALLOWED_HOSTS', '').split(',')
#   Read from env: ALLOWED_HOSTS=example.com,www.example.com
#   .split(',') → converts the comma-separated string to a list

# Security hardening
SECURE_SSL_REDIRECT = True
#   Redirect all HTTP → HTTPS
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
#   Cookies only transmitted over HTTPS
SECURE_HSTS_SECONDS = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True
#   HSTS → browser remembers to always use HTTPS for this domain

# Database credentials from environment variables — never hard-coded
DATABASES['default']['NAME'] = os.environ['DB_NAME']
DATABASES['default']['USER'] = os.environ['DB_USER']
DATABASES['default']['PASSWORD'] = os.environ['DB_PASSWORD']
DATABASES['default']['HOST'] = os.environ.get('DB_HOST', 'db')
#   'db' → default Docker Compose service name for MySQL
```

Activate the correct settings file using `DJANGO_SETTINGS_MODULE`:

```bash
# During development — point to local settings
# Linux / macOS
export DJANGO_SETTINGS_MODULE=mysite.settings.local

# Windows (Command Prompt)
set DJANGO_SETTINGS_MODULE=mysite.settings.local

# Windows (PowerShell)
$env:DJANGO_SETTINGS_MODULE = 'mysite.settings.local'

# In production — point to production settings
export DJANGO_SETTINGS_MODULE=mysite.settings.production
#   Django reads this variable to decide which settings module to import

# You can also pass it on the command line
python manage.py runserver --settings=mysite.settings.local
#   --settings → overrides DJANGO_SETTINGS_MODULE for this command only
```

Keep secrets out of version control using a `.env` file:

```bash
# .env — never commit this file
DJANGO_SECRET_KEY=your-very-long-random-secret-key-here
DB_NAME=mydb_prod
DB_USER=prod_user
DB_PASSWORD=supersecretpassword
ALLOWED_HOSTS=example.com,www.example.com
```

```python
# mysite/settings/base.py — load .env with python-dotenv (pip install python-dotenv)
from dotenv import load_dotenv
load_dotenv()
#   load_dotenv() → reads .env file and sets os.environ variables
#   Must be called before any os.environ.get() calls
```

```gitignore
# .gitignore — always exclude secrets
.env
*.pyc
__pycache__/
staticfiles/
media/
```

### Docker Compose in Depth

> 💡 **Analogy:** Docker Compose is like a **building blueprint** — instead of individually constructing each room (database, web server, cache), you describe the entire building in one file and raise everything at once with a single command.

1️⃣ **WHY** — Production Django deployments involve multiple services: the Django app, MySQL, a cache like Redis, and a reverse proxy like NGINX. Docker Compose lets you define, connect, and orchestrate all of them in one declarative YAML file, ensuring every developer and server runs an identical stack.

2️⃣ **WHEN** — For local development with multiple services, CI/CD pipelines, staging environments, and single-server production deployments.

3️⃣ **HOW**

```dockerfile
# Dockerfile — custom image for the Django application
FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE=1
#   Prevents Python from writing .pyc files to disk
ENV PYTHONUNBUFFERED=1
#   Forces stdout/stderr to be unbuffered — logs appear immediately

WORKDIR /app
#   All subsequent commands run inside /app

# Install system dependencies for mysqlclient
RUN apt-get update && apt-get install -y \
    gcc \
    default-libmysqlclient-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*
#   gcc                        → C compiler for building mysqlclient
#   default-libmysqlclient-dev → MySQL client headers
#   rm -rf /var/lib/apt/lists  → shrink image by removing apt cache

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
#   --no-cache-dir → do not store pip cache (keeps image smaller)

COPY . .
#   Copy all project files into the container

RUN python manage.py collectstatic --noinput
#   Collect static files at build time (not at runtime)

EXPOSE 8000
#   Document that the container listens on port 8000

CMD ["gunicorn", "mysite.wsgi:application", "--bind", "0.0.0.0:8000", "--workers", "3"]
#   Default command — start Gunicorn with 3 workers
```

```yaml
# docker-compose.yml — full multi-service stack
version: '3.8'

services:
  db:
    image: mysql:8.0
    #   Official MySQL 8.0 image from Docker Hub
    restart: unless-stopped
    #   Restart automatically unless explicitly stopped
    environment:
      MYSQL_DATABASE: mydb
      MYSQL_USER: myuser
      MYSQL_PASSWORD: mypassword
      MYSQL_ROOT_PASSWORD: rootpassword
      #   MySQL creates this database and user on first startup
    volumes:
      - mysql_data:/var/lib/mysql
      #   Named volume → data persists across container restarts
    ports:
      - "3306:3306"
      #   Expose MySQL port to host for debugging (remove in production)
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]
      interval: 10s
      timeout: 5s
      retries: 5
      #   Docker pings MySQL every 10s; service is "healthy" after a success

  redis:
    image: redis:7-alpine
    #   Alpine variant → smaller image (~30 MB vs ~130 MB)
    restart: unless-stopped
    ports:
      - "6379:6379"
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5

  web:
    build:
      context: .
      dockerfile: Dockerfile
      #   Build from the Dockerfile in the current directory
    restart: unless-stopped
    ports:
      - "8000:8000"
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
      #   Wait until MySQL and Redis pass their health checks
    environment:
      DJANGO_SETTINGS_MODULE: mysite.settings.production
      DB_HOST: db
      #   'db' → Docker Compose DNS resolves to the db service's container
      DB_NAME: mydb
      DB_USER: myuser
      DB_PASSWORD: mypassword
      REDIS_URL: redis://redis:6379/0
      #   'redis' → Docker Compose DNS resolves to the redis service
    volumes:
      - static_files:/app/staticfiles
      - media_files:/app/media
      #   Share static/media with the nginx service

  nginx:
    image: nginx:1.25-alpine
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - web
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      #   :ro → read-only mount; NGINX only reads the config
      - static_files:/app/staticfiles:ro
      - media_files:/app/media:ro
      #   Same named volumes as web → NGINX serves them directly

volumes:
  mysql_data:
    #   Persistent volume for MySQL data files
  static_files:
    #   Shared volume for collected static files
  media_files:
    #   Shared volume for user-uploaded media
```

Run migrations inside the Docker environment:

```bash
# Build all images and start the stack in detached mode
docker compose up -d --build
#   -d      → detached (runs in background)
#   --build → rebuild images if Dockerfile or code changed

# Run database migrations inside the running web container
docker compose exec web python manage.py migrate
#   exec → run a command in an already-running container
#   web  → the service name from docker-compose.yml

# Create a superuser interactively
docker compose exec web python manage.py createsuperuser

# View logs from all services (follow mode)
docker compose logs -f
#   -f → follow; stream new log lines as they appear

# View logs for a single service
docker compose logs -f web

# Stop all services but keep volumes (data persists)
docker compose down
#   down → stops and removes containers and networks

# Stop all services AND delete volumes (destroys data!)
docker compose down -v
#   -v → also remove named volumes (mysql_data, etc.)

# Restart a single service without rebuilding
docker compose restart web

# Scale a service to multiple instances (for load testing)
docker compose up -d --scale web=3
#   --scale web=3 → run 3 instances of the web service
```

### Serving Django with uWSGI and NGINX

> 💡 **Analogy:** uWSGI is like a **back-kitchen chef** who cooks every meal (handles Python requests), while NGINX is the **front-of-house manager** who greets guests, serves drinks from the bar (static files), and routes food orders to the kitchen. Together they form a complete restaurant.

1️⃣ **WHY** — Django's built-in `runserver` is single-threaded and not designed for production traffic. uWSGI is a battle-tested WSGI application server that manages worker processes, handles concurrency, and communicates efficiently with NGINX via Unix sockets. NGINX serves static files directly without touching Python, handles SSL termination, and buffers slow clients so uWSGI workers are freed quickly.

2️⃣ **WHEN** — When deploying Django to a Linux server where you need fine-grained control over worker processes, memory limits, and protocol-level tuning. Gunicorn is a simpler alternative; uWSGI offers more configuration options for complex deployments.

3️⃣ **HOW**

Install uWSGI:

```bash
pip install uwsgi
#   Installs the uWSGI server with Python plugin support
#   Requires a C compiler (gcc) and Python development headers

# Quick test — run Django through uWSGI on the command line
uwsgi --http :8000 --module mysite.wsgi --master --processes 4
#   --http :8000    → listen on port 8000 over HTTP (for testing)
#   --module        → Python path to the WSGI application
#   --master        → spawn a master process that manages workers
#   --processes 4   → number of worker processes
```

Create a uWSGI configuration file for production:

```ini
; config/uwsgi.ini — production uWSGI configuration
[uwsgi]
; Project paths
chdir = /app
#   chdir → change to the project root directory
module = mysite.wsgi:application
#   module → Python dotted path to the WSGI callable

; Process management
master = true
#   master → spawns a master process that manages workers
processes = 4
#   processes → number of worker processes (2 * CPU cores)
threads = 2
#   threads → threads per process for I/O-bound workloads
enable-threads = true

; Socket for NGINX communication (faster than HTTP)
socket = /tmp/uwsgi.sock
#   Unix socket → NGINX connects here instead of TCP
chmod-socket = 666
#   chmod-socket → allow NGINX to read/write the socket
vacuum = true
#   vacuum → clean up the socket file when uWSGI stops

; Logging
logto = /var/log/uwsgi/mysite.log
#   logto → write logs to a file instead of stdout

; Safety limits
harakiri = 60
#   harakiri → kill workers that take longer than 60 seconds
max-requests = 5000
#   max-requests → recycle workers after 5000 requests (prevents memory leaks)

; Static files (optional — NGINX is faster for this)
; static-map = /static=/app/staticfiles
```

Run uWSGI with the configuration file:

```bash
# Start uWSGI using the ini file
uwsgi --ini config/uwsgi.ini
#   --ini → load configuration from the specified file

# Or run uWSGI in the background
uwsgi --ini config/uwsgi.ini --daemonize /var/log/uwsgi/mysite.log
#   --daemonize → fork to background and write logs to the file
```

Collect static files before configuring NGINX:

```bash
# Collect all static files into STATIC_ROOT
python manage.py collectstatic --noinput
#   --noinput → skip the confirmation prompt
#   Copies files from each app's static/ dir into settings.STATIC_ROOT
#   NGINX will serve these files directly
```

Configure NGINX as a reverse proxy for uWSGI:

```nginx
# /etc/nginx/sites-available/mysite.conf
upstream django {
    server unix:///tmp/uwsgi.sock;
    #   Connect to uWSGI via Unix socket (must match uwsgi.ini)
}

server {
    listen 80;
    server_name example.com www.example.com;
    #   server_name → the domain(s) this block responds to
    charset utf-8;

    client_max_body_size 10M;
    #   Maximum upload size — increase for large file uploads

    # Serve static files directly from disk (bypass uWSGI)
    location /static/ {
        alias /app/staticfiles/;
        #   alias → maps the URL path to a directory on disk
        expires 30d;
        #   expires → browser caches static files for 30 days
        access_log off;
        #   access_log off → don't log static file requests
    }

    # Serve user-uploaded media files
    location /media/ {
        alias /app/media/;
        expires 7d;
    }

    # Proxy all other requests to uWSGI
    location / {
        uwsgi_pass django;
        #   uwsgi_pass → forward requests using the uwsgi protocol
        include uwsgi_params;
        #   uwsgi_params → standard set of uwsgi variables
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

Enable the site and restart NGINX:

```bash
# Create a symlink to enable the site
sudo ln -s /etc/nginx/sites-available/mysite.conf /etc/nginx/sites-enabled/
#   sites-enabled → NGINX reads configs from this directory

# Test NGINX configuration for syntax errors
sudo nginx -t
#   -t → test the configuration and report errors without starting

# Reload NGINX to apply the new configuration
sudo systemctl reload nginx
#   reload → graceful restart; existing connections are not dropped
```

> **Note:** Gunicorn is a popular alternative to uWSGI. It is simpler to configure and works well for most Django projects. Use Gunicorn if you prefer fewer configuration options, and uWSGI if you need advanced features like cron-like task scheduling, cheaper worker recycling, or the uwsgi binary protocol.

### SSL/TLS Certificates

> 💡 **Analogy:** SSL/TLS is like sending a letter in a **tamper-proof, locked envelope** instead of a postcard — anyone who intercepts it in transit sees only a sealed box, not the message inside.

1️⃣ **WHY** — Without SSL/TLS, data between the browser and server travels in plaintext. Passwords, session cookies, and personal information can be intercepted by anyone on the same network. Modern browsers flag HTTP sites as "Not Secure," and search engines penalize them in rankings.

2️⃣ **WHEN** — Always in production. For local development, a self-signed certificate lets you test HTTPS-dependent features like secure cookies and HSTS before deploying.

3️⃣ **HOW**

First, verify your Django project is ready for production with the built-in check:

```bash
# Run Django's deployment security checklist
python manage.py check --deploy
#   Checks for common security misconfigurations
#   Reports warnings like:
#     ?: (security.W004) You have not set a value for SECURE_HSTS_SECONDS
#     ?: (security.W008) SECURE_SSL_REDIRECT is not set to True
#     ?: (security.W012) SESSION_COOKIE_SECURE is not set to True
```

Configure Django for SSL/TLS in production settings:

```python
# mysite/settings/production.py — SSL/TLS settings
from .base import *

DEBUG = False
ALLOWED_HOSTS = os.environ.get('ALLOWED_HOSTS', '').split(',')

# --- SSL/TLS configuration ---

SECURE_SSL_REDIRECT = True
#   Redirect every HTTP request to HTTPS automatically

SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
#   Trust the X-Forwarded-Proto header set by NGINX
#   Required when NGINX terminates SSL and forwards HTTP to Django

SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
#   Cookies are only sent over HTTPS connections

SECURE_HSTS_SECONDS = 31536000
#   31536000 = 1 year; tells browsers to always use HTTPS for this domain
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
#   Apply HSTS to all subdomains (e.g., api.example.com)
SECURE_HSTS_PRELOAD = True
#   Allow the domain to be included in browser HSTS preload lists

SECURE_CONTENT_TYPE_NOSNIFF = True
#   Prevent browsers from MIME-sniffing the content type

SECURE_BROWSER_XSS_FILTER = True
#   Enable the browser's built-in XSS filter (legacy, but harmless)
```

Create a self-signed certificate for local development and testing:

```bash
# Generate a self-signed SSL certificate (valid for 365 days)
openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/nginx-selfsigned.key \
    -out /etc/ssl/certs/nginx-selfsigned.crt \
    -subj "/C=US/ST=State/L=City/O=Dev/CN=localhost"
#   -x509     → generate a self-signed certificate (not a CSR)
#   -nodes    → no passphrase on the private key
#   -days 365 → certificate validity period
#   -newkey rsa:2048 → generate a new 2048-bit RSA key
#   -subj     → certificate subject (avoids interactive prompts)

# Generate Diffie-Hellman parameters for stronger security
openssl dhparam -out /etc/ssl/certs/dhparam.pem 2048
#   dhparam → improves forward secrecy for TLS connections
```

Configure NGINX for HTTPS with SSL termination:

```nginx
# /etc/nginx/sites-available/mysite.conf — HTTPS configuration

# Redirect all HTTP traffic to HTTPS
server {
    listen 80;
    server_name example.com www.example.com;
    return 301 https://$host$request_uri;
    #   301 → permanent redirect; browsers cache this
    #   $host → preserves the original hostname
    #   $request_uri → preserves the original path and query string
}

# HTTPS server block
server {
    listen 443 ssl;
    server_name example.com www.example.com;

    # SSL certificate paths
    ssl_certificate /etc/ssl/certs/nginx-selfsigned.crt;
    ssl_certificate_key /etc/ssl/private/nginx-selfsigned.key;
    #   For production, replace with Let's Encrypt paths:
    #   ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    #   ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    # Strong SSL settings
    ssl_protocols TLSv1.2 TLSv1.3;
    #   Only allow modern TLS versions (disable SSLv3, TLSv1.0, TLSv1.1)
    ssl_prefer_server_ciphers on;
    #   Server chooses the cipher suite, not the client
    ssl_dhparam /etc/ssl/certs/dhparam.pem;
    #   Use custom Diffie-Hellman parameters

    client_max_body_size 10M;

    # Static and media files
    location /static/ {
        alias /app/staticfiles/;
        expires 30d;
    }

    location /media/ {
        alias /app/media/;
        expires 7d;
    }

    # Proxy to uWSGI or Gunicorn
    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        #   X-Forwarded-Proto → tells Django the original request was HTTPS
    }
}
```

For production, use Let's Encrypt to get free, trusted certificates:

```bash
# Install Certbot (Let's Encrypt client) on Ubuntu
sudo apt update && sudo apt install certbot python3-certbot-nginx
#   certbot             → the ACME client that talks to Let's Encrypt
#   python3-certbot-nginx → plugin that auto-configures NGINX

# Obtain a certificate and auto-configure NGINX
sudo certbot --nginx -d example.com -d www.example.com
#   --nginx → use the NGINX plugin to install the certificate
#   -d      → domain names to include in the certificate
#   Certbot modifies your NGINX config to add ssl_certificate directives

# Test automatic renewal
sudo certbot renew --dry-run
#   --dry-run → simulates renewal without making changes
#   Let's Encrypt certificates expire every 90 days
#   Certbot sets up a systemd timer or cron job for auto-renewal

# Verify the timer is active
sudo systemctl list-timers | grep certbot
#   Should show a timer that runs certbot renew twice daily
```

### Serving Django Channels with Daphne

> 💡 **Analogy:** If Gunicorn/uWSGI is a **telephone operator** handling one call at a time per line, Daphne is a **group video-call host** — it can keep many WebSocket connections open simultaneously, streaming data back and forth in real time.

1️⃣ **WHY** — Django Channels extends Django to handle WebSockets, long-polling, and other asynchronous protocols. Daphne is the reference ASGI (Asynchronous Server Gateway Interface) server built for Channels. It manages persistent WebSocket connections that traditional WSGI servers like Gunicorn and uWSGI cannot handle.

2️⃣ **WHEN** — When your Django project uses Channels for real-time features like chat, live notifications, collaborative editing, or live dashboards. You run Daphne alongside Gunicorn or uWSGI — Daphne handles ASGI/WebSocket traffic while the WSGI server handles regular HTTP requests.

3️⃣ **HOW**

Install Daphne and Django Channels:

```bash
pip install daphne channels channels-redis
#   daphne         → ASGI server for Django Channels
#   channels       → Django Channels framework
#   channels-redis → Redis-backed channel layer for cross-process messaging
```

Configure your Django project for ASGI:

```python
# mysite/asgi.py — ASGI application entry point
import os
from django.core.asgi import get_asgi_application
from channels.routing import ProtocolTypeRouter, URLRouter
from channels.auth import AuthMiddlewareStack

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings.production')

django_asgi_app = get_asgi_application()
#   get_asgi_application() → handles standard HTTP requests via ASGI

from chat.routing import websocket_urlpatterns
#   Import after Django setup to avoid AppRegistryNotReady errors

application = ProtocolTypeRouter({
    'http': django_asgi_app,
    #   HTTP requests → standard Django views
    'websocket': AuthMiddlewareStack(
        URLRouter(websocket_urlpatterns)
    ),
    #   WebSocket requests → routed through authentication middleware
    #   AuthMiddlewareStack → populates scope['user'] from session cookies
})
```

```python
# mysite/settings/base.py — add Channels configuration
INSTALLED_APPS = [
    'daphne',
    #   Must be listed BEFORE django.contrib.staticfiles
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'channels',
    'chat',
]

ASGI_APPLICATION = 'mysite.asgi.application'
#   Points to the ProtocolTypeRouter in asgi.py

CHANNEL_LAYERS = {
    'default': {
        'BACKEND': 'channels_redis.core.RedisChannelLayer',
        'CONFIG': {
            'hosts': [os.environ.get('REDIS_URL', 'redis://127.0.0.1:6379/0')],
            #   Redis acts as the message broker between Daphne workers
        },
    },
}
```

Run Daphne from the command line:

```bash
# Start Daphne directly (for testing)
daphne -b 0.0.0.0 -p 9000 mysite.asgi:application
#   -b 0.0.0.0 → bind to all network interfaces
#   -p 9000    → listen on port 9000
#   mysite.asgi:application → the ASGI application callable
```

Configure Daphne in Docker Compose alongside Gunicorn:

```yaml
# docker-compose.yml — running WSGI and ASGI side by side
services:
  db:
    image: mysql:8.0
    restart: unless-stopped
    environment:
      MYSQL_DATABASE: mydb
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

  redis:
    image: redis:7-alpine
    restart: unless-stopped
    healthcheck:
      test: ["CMD", "redis-cli", "ping"]
      interval: 10s
      timeout: 5s
      retries: 5

  web:
    build: .
    command: gunicorn mysite.wsgi:application --bind 0.0.0.0:8000 --workers 3
    #   Gunicorn handles regular HTTP requests (views, API, admin)
    restart: unless-stopped
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    environment:
      DJANGO_SETTINGS_MODULE: mysite.settings.production
      DB_HOST: db
      DB_NAME: mydb
      DB_USER: myuser
      DB_PASSWORD: mypassword
      REDIS_URL: redis://redis:6379/0

  daphne:
    build: .
    command: daphne -b 0.0.0.0 -p 9000 mysite.asgi:application
    #   Daphne handles WebSocket connections on port 9000
    restart: unless-stopped
    depends_on:
      db:
        condition: service_healthy
      redis:
        condition: service_healthy
    environment:
      DJANGO_SETTINGS_MODULE: mysite.settings.production
      DB_HOST: db
      DB_NAME: mydb
      DB_USER: myuser
      DB_PASSWORD: mypassword
      REDIS_URL: redis://redis:6379/0

  nginx:
    image: nginx:1.25-alpine
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    depends_on:
      - web
      - daphne
    volumes:
      - ./nginx/default.conf:/etc/nginx/conf.d/default.conf:ro
      - static_files:/app/staticfiles:ro
      - media_files:/app/media:ro

volumes:
  mysql_data:
  static_files:
  media_files:
```

Configure NGINX to route WebSocket traffic to Daphne and HTTP traffic to Gunicorn:

```nginx
# nginx/default.conf — routing HTTP and WebSocket traffic

upstream wsgi_server {
    server web:8000;
    #   Gunicorn — handles regular Django HTTP requests
}

upstream asgi_server {
    server daphne:9000;
    #   Daphne — handles WebSocket connections
}

server {
    listen 80;
    server_name example.com;

    location /static/ {
        alias /app/staticfiles/;
        expires 30d;
    }

    location /media/ {
        alias /app/media/;
        expires 7d;
    }

    # WebSocket connections → Daphne
    location /ws/ {
        proxy_pass http://asgi_server;
        proxy_http_version 1.1;
        #   HTTP/1.1 required for WebSocket upgrade
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        #   Upgrade + Connection headers → enable the WebSocket handshake
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_read_timeout 86400;
        #   86400s = 24h; prevent NGINX from closing idle WebSocket connections
    }

    # All other requests → Gunicorn
    location / {
        proxy_pass http://wsgi_server;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

For secure WebSocket connections (wss://), use the HTTPS server block:

```nginx
# HTTPS server block with secure WebSocket support
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;

    # wss:// connections are regular WebSocket over TLS
    # NGINX terminates SSL and forwards plain WebSocket to Daphne
    location /ws/ {
        proxy_pass http://asgi_server;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        #   X-Forwarded-Proto → Daphne knows the original connection was wss://
        proxy_read_timeout 86400;
    }

    location / {
        proxy_pass http://wsgi_server;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

```javascript
// In your frontend JavaScript — connect with wss:// in production
const protocol = window.location.protocol === 'https:' ? 'wss://' : 'ws://';
//   Use wss:// when the page is loaded over HTTPS
const socket = new WebSocket(protocol + window.location.host + '/ws/chat/room1/');
//   The /ws/ prefix routes through NGINX to Daphne
```

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
