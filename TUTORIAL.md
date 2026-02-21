# Django with MySQL — Comprehensive Tutorial

## Table of Contents

- [Part 1: Basics](#part-1-basics)
  - [What is Django?](#what-is-django)
  - [Setting Up the Development Environment](#setting-up-the-development-environment)
  - [Creating Your First Django Project](#creating-your-first-django-project)
  - [Understanding the Project Structure](#understanding-the-project-structure)
- [Part 2: Models and Databases](#part-2-models-and-databases)
  - [Configuring MySQL](#configuring-mysql)
  - [Defining Models](#defining-models)
  - [Migrations](#migrations)
  - [The Django ORM](#the-django-orm)
- [Part 3: Views and URLs](#part-3-views-and-urls)
  - [Function-Based Views](#function-based-views)
  - [Class-Based Views](#class-based-views)
  - [URL Routing](#url-routing)
- [Part 4: Templates](#part-4-templates)
  - [Template Language Basics](#template-language-basics)
  - [Template Inheritance](#template-inheritance)
  - [Static Files](#static-files)
- [Part 5: Forms and Validation](#part-5-forms-and-validation)
  - [Django Forms](#django-forms)
  - [ModelForms](#modelforms)
  - [Validation](#validation)
- [Part 6: Authentication and Authorization](#part-6-authentication-and-authorization)
  - [User Model](#user-model)
  - [Login and Logout](#login-and-logout)
  - [Permissions and Groups](#permissions-and-groups)
- [Part 7: Django Admin](#part-7-django-admin)
  - [Registering Models](#registering-models)
  - [Customizing the Admin Interface](#customizing-the-admin-interface)
- [Part 8: REST APIs with Django REST Framework](#part-8-rest-apis-with-django-rest-framework)
  - [Serializers](#serializers)
  - [API Views and Viewsets](#api-views-and-viewsets)
  - [Authentication for APIs](#authentication-for-apis)
- [Part 9: Testing](#part-9-testing)
  - [Unit Tests](#unit-tests)
  - [Integration Tests](#integration-tests)
  - [Testing with MySQL](#testing-with-mysql)
- [Part 10: Deployment](#part-10-deployment)
  - [Preparing for Production](#preparing-for-production)
  - [Deploying with Gunicorn and Nginx](#deploying-with-gunicorn-and-nginx)
- [Exercises](#exercises)
- [Projects](#projects)
- [Cheat Sheet](#cheat-sheet)
- [Further Reading](#further-reading)

---

## Part 1: Basics

### What is Django?

Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. It follows the **Model-View-Template (MVT)** pattern and comes with many built-in features such as an ORM, authentication system, and admin interface.

Key features:

- **Batteries included** — authentication, URL routing, template engine, ORM, and more out of the box.
- **Security** — protects against common vulnerabilities like SQL injection, XSS, and CSRF.
- **Scalability** — used by large-scale sites such as Instagram and Mozilla.

### Setting Up the Development Environment

1. **Install Python 3.8+**

   ```bash
   python3 --version
   ```

2. **Create a virtual environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # Linux/macOS
   venv\Scripts\activate      # Windows
   ```

3. **Install Django**

   ```bash
   pip install django
   ```

4. **Install MySQL client library**

   ```bash
   pip install mysqlclient
   ```

5. **Verify installation**

   ```bash
   python -m django --version
   ```

### Creating Your First Django Project

```bash
django-admin startproject mysite
cd mysite
python manage.py runserver
```

Visit `http://127.0.0.1:8000/` in your browser to see the default Django welcome page.

### Understanding the Project Structure

```
mysite/
├── manage.py           # Command-line utility
└── mysite/
    ├── __init__.py     # Marks directory as a Python package
    ├── settings.py     # Project settings
    ├── urls.py         # Root URL configuration
    ├── asgi.py         # ASGI entry point
    └── wsgi.py         # WSGI entry point
```

---

## Part 2: Models and Databases

### Configuring MySQL

Edit `mysite/settings.py` to use MySQL:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',
        'USER': 'myuser',
        'PASSWORD': 'mypassword',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```

> **Tip:** Store sensitive credentials in environment variables or a `.env` file rather than hard-coding them.

### Defining Models

Create an app and define models:

```bash
python manage.py startapp blog
```

```python
# blog/models.py
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    body = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

Add `'blog'` to `INSTALLED_APPS` in `settings.py`.

### Migrations

```bash
python manage.py makemigrations blog
python manage.py migrate
```

Migrations translate model changes into database schema operations.

### The Django ORM

```python
# Create
post = Post.objects.create(title="Hello", body="World")

# Read
all_posts = Post.objects.all()
post = Post.objects.get(pk=1)

# Update
post.title = "Updated Title"
post.save()

# Delete
post.delete()

# Filter and chain
recent = Post.objects.filter(created_at__year=2026).order_by('-created_at')
```

---

## Part 3: Views and URLs

### Function-Based Views

```python
# blog/views.py
from django.http import HttpResponse
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    output = ', '.join([p.title for p in posts])
    return HttpResponse(output)
```

### Class-Based Views

```python
# blog/views.py
from django.views.generic import ListView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'
```

### URL Routing

```python
# blog/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
]
```

Include the app URLs in the project:

```python
# mysite/urls.py
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('blog/', include('blog.urls')),
]
```

---

## Part 4: Templates

### Template Language Basics

```html
<!-- blog/templates/blog/post_list.html -->
<h1>Blog Posts</h1>
<ul>
{% for post in posts %}
    <li>{{ post.title }} — {{ post.created_at|date:"M d, Y" }}</li>
{% empty %}
    <li>No posts yet.</li>
{% endfor %}
</ul>
```

### Template Inheritance

**Base template:**

```html
<!-- templates/base.html -->
<!DOCTYPE html>
<html>
<head><title>{% block title %}My Site{% endblock %}</title></head>
<body>
  <header><h1>My Site</h1></header>
  <main>{% block content %}{% endblock %}</main>
</body>
</html>
```

**Child template:**

```html
<!-- blog/templates/blog/post_list.html -->
{% extends "base.html" %}

{% block title %}Blog{% endblock %}

{% block content %}
<ul>
{% for post in posts %}
    <li>{{ post.title }}</li>
{% endfor %}
</ul>
{% endblock %}
```

### Static Files

```python
# settings.py
STATIC_URL = '/static/'
```

```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
```

---

## Part 5: Forms and Validation

### Django Forms

```python
# blog/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

### ModelForms

```python
# blog/forms.py
from django.forms import ModelForm
from .models import Post

class PostForm(ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'body']
```

Using a form in a view:

```python
# blog/views.py
from django.shortcuts import render, redirect
from .forms import PostForm

def post_create(request):
    if request.method == 'POST':
        form = PostForm(request.POST)
        if form.is_valid():
            form.save()
            return redirect('post_list')
    else:
        form = PostForm()
    return render(request, 'blog/post_form.html', {'form': form})
```

### Validation

```python
# blog/forms.py
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)

    def clean_name(self):
        name = self.cleaned_data['name']
        if len(name) < 2:
            raise forms.ValidationError("Name must be at least 2 characters.")
        return name
```

---

## Part 6: Authentication and Authorization

### User Model

Django provides a built-in `User` model. To create a superuser:

```bash
python manage.py createsuperuser
```

### Login and Logout

```python
# mysite/urls.py
from django.contrib.auth import views as auth_views

urlpatterns = [
    path('login/', auth_views.LoginView.as_view(), name='login'),
    path('logout/', auth_views.LogoutView.as_view(), name='logout'),
]
```

Add `LOGIN_REDIRECT_URL = '/'` to `settings.py`.

### Permissions and Groups

```python
from django.contrib.auth.decorators import login_required, permission_required

@login_required
def dashboard(request):
    return render(request, 'dashboard.html')

@permission_required('blog.add_post')
def create_post(request):
    ...
```

---

## Part 7: Django Admin

### Registering Models

```python
# blog/admin.py
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

### Customizing the Admin Interface

```python
# blog/admin.py
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'created_at', 'updated_at')
    search_fields = ('title', 'body')
    list_filter = ('created_at',)
    ordering = ('-created_at',)
```

---

## Part 8: REST APIs with Django REST Framework

Install Django REST Framework:

```bash
pip install djangorestframework
```

Add `'rest_framework'` to `INSTALLED_APPS`.

### Serializers

```python
# blog/serializers.py
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'body', 'created_at', 'updated_at']
```

### API Views and Viewsets

```python
# blog/views.py
from rest_framework import viewsets
from .models import Post
from .serializers import PostSerializer

class PostViewSet(viewsets.ModelViewSet):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

```python
# blog/urls.py
from rest_framework.routers import DefaultRouter
from .views import PostViewSet

router = DefaultRouter()
router.register(r'posts', PostViewSet)

urlpatterns = router.urls
```

### Authentication for APIs

```python
# settings.py
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.SessionAuthentication',
        'rest_framework.authentication.TokenAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
}
```

---

## Part 9: Testing

### Unit Tests

```python
# blog/tests.py
from django.test import TestCase
from .models import Post

class PostModelTest(TestCase):
    def setUp(self):
        Post.objects.create(title="Test", body="Body text")

    def test_post_str(self):
        post = Post.objects.first()
        self.assertEqual(str(post), "Test")
```

### Integration Tests

```python
from django.test import TestCase, Client

class PostViewTest(TestCase):
    def setUp(self):
        self.client = Client()
        Post.objects.create(title="Hello", body="World")

    def test_post_list_view(self):
        response = self.client.get('/blog/')
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, "Hello")
```

### Testing with MySQL

By default Django creates a test database. For MySQL, ensure the database user has `CREATE DATABASE` privileges:

```bash
python manage.py test
```

You can also configure a separate test database in `settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',
        'TEST': {
            'NAME': 'test_mydatabase',
        },
        ...
    }
}
```

---

## Part 10: Deployment

### Preparing for Production

1. Set `DEBUG = False` in `settings.py`.
2. Configure `ALLOWED_HOSTS`.
3. Collect static files:

   ```bash
   python manage.py collectstatic
   ```

4. Use environment variables for secrets:

   ```python
   import os
   SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')
   ```

### Deploying with Gunicorn and Nginx

Install Gunicorn:

```bash
pip install gunicorn
```

Run with Gunicorn:

```bash
gunicorn mysite.wsgi:application --bind 0.0.0.0:8000
```

A minimal Nginx configuration:

```nginx
server {
    listen 80;
    server_name example.com;

    location /static/ {
        alias /path/to/staticfiles/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---

## Exercises

1. **Create a blog app** — Build a blog application with models for `Post` and `Comment`. Implement list, detail, create, update, and delete views.
2. **User registration** — Add a signup page using Django's `UserCreationForm`. Redirect new users to the login page after registration.
3. **Search feature** — Add a search bar that filters blog posts by title using `icontains` lookups.
4. **Pagination** — Use Django's `Paginator` class to paginate the post list view (e.g., 5 posts per page).
5. **REST API** — Expose the blog posts through a REST API using Django REST Framework. Add filtering by creation date.
6. **Custom template tags** — Write a custom template tag that displays the total number of posts in the sidebar.
7. **File uploads** — Allow users to attach an image to each blog post. Serve uploaded media files during development.

---

## Projects

### Project 1: Task Manager

Build a task management application with the following features:

- User authentication (register, login, logout).
- CRUD operations for tasks (title, description, status, due date).
- Filter tasks by status (pending, in progress, done).
- MySQL database backend.

### Project 2: E-Commerce Store

Build a simple e-commerce storefront:

- Product catalog with categories.
- Shopping cart using Django sessions.
- Order checkout with form validation.
- Admin interface for managing products and orders.
- REST API for product listing.

### Project 3: Social Bookmarking Site

Build a site where users can save and share bookmarks:

- User accounts with profile pages.
- Bookmark model with URL, title, description, and tags.
- Tag-based filtering and search.
- Public and private bookmarks.
- REST API for creating and listing bookmarks.

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

### Model Field Types

| Field | Description |
|---|---|
| `CharField(max_length=N)` | Short text |
| `TextField()` | Long text |
| `IntegerField()` | Integer |
| `FloatField()` | Floating-point number |
| `BooleanField()` | True/False |
| `DateTimeField()` | Date and time |
| `ForeignKey(Model, on_delete=...)` | Many-to-one relationship |
| `ManyToManyField(Model)` | Many-to-many relationship |
| `EmailField()` | Email address |
| `URLField()` | URL |
| `FileField(upload_to='...')` | File upload |
| `ImageField(upload_to='...')` | Image upload |

### QuerySet Methods

| Method | Example |
|---|---|
| `all()` | `Post.objects.all()` |
| `filter()` | `Post.objects.filter(title__icontains='django')` |
| `exclude()` | `Post.objects.exclude(status='draft')` |
| `get()` | `Post.objects.get(pk=1)` |
| `create()` | `Post.objects.create(title='New')` |
| `order_by()` | `Post.objects.order_by('-created_at')` |
| `count()` | `Post.objects.count()` |
| `exists()` | `Post.objects.filter(pk=1).exists()` |
| `values()` | `Post.objects.values('title', 'created_at')` |
| `first()` / `last()` | `Post.objects.first()` |

---

## Further Reading

- [Django Official Documentation](https://docs.djangoproject.com/)
- [Django REST Framework Documentation](https://www.django-rest-framework.org/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Django Girls Tutorial](https://tutorial.djangogirls.org/)
- [Two Scoops of Django (book)](https://www.feldroy.com/books/two-scoops-of-django-3-x)
- [Classy Class-Based Views](https://ccbv.co.uk/) — reference for all Django CBVs
- [Django Packages](https://djangopackages.org/) — reusable app directory
