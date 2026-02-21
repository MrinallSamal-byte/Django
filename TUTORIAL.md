# Django with MySQL — Comprehensive Tutorial

## Table of Contents

- [Part 1: Basics](#part-1-basics)
  - [What is Django?](#what-is-django)
  - [Setting Up Your Environment](#setting-up-your-environment)
  - [Creating a Django Project](#creating-a-django-project)
  - [Running the Development Server](#running-the-development-server)
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
- [Part 5: Forms](#part-5-forms)
  - [Django Forms](#django-forms)
  - [Model Forms](#model-forms)
  - [Form Validation](#form-validation)
- [Part 6: Authentication and Authorization](#part-6-authentication-and-authorization)
  - [User Model](#user-model)
  - [Login and Logout](#login-and-logout)
  - [Permissions and Groups](#permissions-and-groups)
- [Part 7: Django Admin](#part-7-django-admin)
  - [Registering Models](#registering-models)
  - [Customizing the Admin Interface](#customizing-the-admin-interface)
- [Part 8: REST APIs with Django REST Framework](#part-8-rest-apis-with-django-rest-framework)
  - [Serializers](#serializers)
  - [API Views](#api-views)
  - [Authentication for APIs](#authentication-for-apis)
- [Part 9: Testing](#part-9-testing)
  - [Writing Unit Tests](#writing-unit-tests)
  - [Testing Views](#testing-views)
  - [Using the Test Client](#using-the-test-client)
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

Django is a high-level Python web framework that encourages rapid development and clean, pragmatic design. It follows the **model–template–view (MTV)** architectural pattern and includes built-in support for database operations, URL routing, template rendering, form handling, authentication, and much more.

Key features:

- **Batteries included** — admin panel, ORM, authentication, and more out of the box.
- **Security** — built-in protection against SQL injection, XSS, CSRF, and clickjacking.
- **Scalability** — used by large-scale sites such as Instagram and Pinterest.

### Setting Up Your Environment

1. **Install Python 3.10+**

   ```bash
   python3 --version
   ```

2. **Create a virtual environment**

   ```bash
   python3 -m venv venv
   source venv/bin/activate   # Linux / macOS
   venv\Scripts\activate      # Windows
   ```

3. **Install Django**

   ```bash
   pip install django
   ```

4. **Install the MySQL client library**

   ```bash
   pip install mysqlclient
   ```

   > On Ubuntu/Debian you may first need: `sudo apt-get install python3-dev default-libmysqlclient-dev build-essential`

5. **Verify installations**

   ```bash
   python -m django --version
   ```

### Creating a Django Project

```bash
django-admin startproject myproject
cd myproject
```

This creates the following structure:

```
myproject/
├── manage.py
└── myproject/
    ├── __init__.py
    ├── asgi.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

### Running the Development Server

```bash
python manage.py runserver
```

Open <http://127.0.0.1:8000/> in your browser to see the default Django welcome page.

---

## Part 2: Models and Databases

### Configuring MySQL

Edit `myproject/settings.py`:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'my_database',
        'USER': 'my_user',
        'PASSWORD': 'my_password',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}
```

Create the database in MySQL beforehand:

```sql
CREATE DATABASE my_database CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

### Defining Models

Create an app first:

```bash
python manage.py startapp blog
```

Add it to `INSTALLED_APPS` in `settings.py`:

```python
INSTALLED_APPS = [
    # ...
    'blog',
]
```

Define a model in `blog/models.py`:

```python
from django.db import models

class Post(models.Model):
    title = models.CharField(max_length=200)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self):
        return self.title
```

### Migrations

```bash
python manage.py makemigrations blog
python manage.py migrate
```

### The Django ORM

```python
# Create
post = Post.objects.create(title="Hello", content="World")

# Read
all_posts = Post.objects.all()
single = Post.objects.get(pk=1)

# Update
single.title = "Updated Title"
single.save()

# Delete
single.delete()

# Filter and chain
recent = Post.objects.filter(created_at__year=2026).order_by('-created_at')
```

---

## Part 3: Views and URLs

### Function-Based Views

`blog/views.py`:

```python
from django.http import HttpResponse
from django.shortcuts import render, get_object_or_404
from .models import Post

def post_list(request):
    posts = Post.objects.all()
    return render(request, 'blog/post_list.html', {'posts': posts})

def post_detail(request, pk):
    post = get_object_or_404(Post, pk=pk)
    return render(request, 'blog/post_detail.html', {'post': post})
```

### Class-Based Views

```python
from django.views.generic import ListView, DetailView
from .models import Post

class PostListView(ListView):
    model = Post
    template_name = 'blog/post_list.html'
    context_object_name = 'posts'

class PostDetailView(DetailView):
    model = Post
    template_name = 'blog/post_detail.html'
    context_object_name = 'post'
```

### URL Routing

`blog/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.post_list, name='post_list'),
    path('post/<int:pk>/', views.post_detail, name='post_detail'),
]
```

Include in `myproject/urls.py`:

```python
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

Create `blog/templates/blog/post_list.html`:

```html
<!DOCTYPE html>
<html>
<head><title>Blog</title></head>
<body>
  <h1>Posts</h1>
  {% for post in posts %}
    <article>
      <h2><a href="{% url 'post_detail' post.pk %}">{{ post.title }}</a></h2>
      <p>{{ post.content|truncatewords:30 }}</p>
    </article>
  {% empty %}
    <p>No posts yet.</p>
  {% endfor %}
</body>
</html>
```

### Template Inheritance

`blog/templates/blog/base.html`:

```html
<!DOCTYPE html>
<html>
<head>
  <title>{% block title %}My Blog{% endblock %}</title>
  {% load static %}
  <link rel="stylesheet" href="{% static 'blog/style.css' %}">
</head>
<body>
  <header><h1>My Blog</h1></header>
  <main>{% block content %}{% endblock %}</main>
</body>
</html>
```

Child template:

```html
{% extends 'blog/base.html' %}

{% block title %}{{ post.title }}{% endblock %}

{% block content %}
  <article>
    <h2>{{ post.title }}</h2>
    <p>{{ post.content }}</p>
  </article>
{% endblock %}
```

### Static Files

Place CSS, JavaScript, and images in `blog/static/blog/`. In templates, load them with:

```html
{% load static %}
<link rel="stylesheet" href="{% static 'blog/style.css' %}">
```

Run `collectstatic` for production:

```bash
python manage.py collectstatic
```

---

## Part 5: Forms

### Django Forms

`blog/forms.py`:

```python
from django import forms

class ContactForm(forms.Form):
    name = forms.CharField(max_length=100)
    email = forms.EmailField()
    message = forms.CharField(widget=forms.Textarea)
```

### Model Forms

```python
from django import forms
from .models import Post

class PostForm(forms.ModelForm):
    class Meta:
        model = Post
        fields = ['title', 'content']
```

### Form Validation

```python
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

Using a form in a view:

```python
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

---

## Part 6: Authentication and Authorization

### User Model

Django provides a built-in `User` model in `django.contrib.auth.models`. You can extend it with a profile model:

```python
from django.db import models
from django.contrib.auth.models import User

class Profile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE)
    bio = models.TextField(blank=True)
```

### Login and Logout

Add Django's auth URLs in `myproject/urls.py`:

```python
urlpatterns = [
    path('accounts/', include('django.contrib.auth.urls')),
    # ...
]
```

Create `registration/login.html`:

```html
{% extends 'blog/base.html' %}

{% block content %}
  <h2>Login</h2>
  <form method="post">
    {% csrf_token %}
    {{ form.as_p }}
    <button type="submit">Log in</button>
  </form>
{% endblock %}
```

Protect views with `@login_required`:

```python
from django.contrib.auth.decorators import login_required

@login_required
def post_create(request):
    # ...
```

### Permissions and Groups

```python
from django.contrib.auth.decorators import permission_required

@permission_required('blog.add_post')
def post_create(request):
    # ...
```

---

## Part 7: Django Admin

### Registering Models

`blog/admin.py`:

```python
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```

Create a superuser:

```bash
python manage.py createsuperuser
```

Visit <http://127.0.0.1:8000/admin/> to manage data.

### Customizing the Admin Interface

```python
from django.contrib import admin
from .models import Post

@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ('title', 'created_at', 'updated_at')
    search_fields = ('title', 'content')
    list_filter = ('created_at',)
    ordering = ('-created_at',)
```

---

## Part 8: REST APIs with Django REST Framework

Install Django REST Framework:

```bash
pip install djangorestframework
```

Add to `INSTALLED_APPS`:

```python
INSTALLED_APPS = [
    # ...
    'rest_framework',
]
```

### Serializers

`blog/serializers.py`:

```python
from rest_framework import serializers
from .models import Post

class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = Post
        fields = ['id', 'title', 'content', 'created_at', 'updated_at']
```

### API Views

```python
from rest_framework import generics
from .models import Post
from .serializers import PostSerializer

class PostListCreateAPI(generics.ListCreateAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer

class PostRetrieveUpdateDestroyAPI(generics.RetrieveUpdateDestroyAPIView):
    queryset = Post.objects.all()
    serializer_class = PostSerializer
```

Wire up the URLs:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('api/posts/', views.PostListCreateAPI.as_view(), name='post_api_list'),
    path('api/posts/<int:pk>/', views.PostRetrieveUpdateDestroyAPI.as_view(), name='post_api_detail'),
]
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
        'rest_framework.permissions.IsAuthenticatedOrReadOnly',
    ],
}
```

---

## Part 9: Testing

### Writing Unit Tests

`blog/tests.py`:

```python
from django.test import TestCase
from .models import Post

class PostModelTest(TestCase):
    def setUp(self):
        self.post = Post.objects.create(title="Test", content="Content")

    def test_string_representation(self):
        self.assertEqual(str(self.post), "Test")

    def test_post_creation(self):
        self.assertIsNotNone(self.post.created_at)
```

### Testing Views

```python
from django.test import TestCase
from django.urls import reverse
from .models import Post

class PostViewTest(TestCase):
    def setUp(self):
        self.post = Post.objects.create(title="Test", content="Content")

    def test_post_list_view(self):
        response = self.client.get(reverse('post_list'))
        self.assertEqual(response.status_code, 200)
        self.assertContains(response, "Test")
```

### Using the Test Client

```bash
python manage.py test blog
```

---

## Part 10: Deployment

### Preparing for Production

1. Set `DEBUG = False` in `settings.py`.
2. Configure `ALLOWED_HOSTS`.
3. Use environment variables for secrets:

   ```python
   import os
   SECRET_KEY = os.environ.get('DJANGO_SECRET_KEY')
   ```

4. Collect static files:

   ```bash
   python manage.py collectstatic
   ```

### Deploying with Gunicorn and Nginx

Install Gunicorn:

```bash
pip install gunicorn
```

Run:

```bash
gunicorn myproject.wsgi:application --bind 0.0.0.0:8000
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

1. **Hello World View** — Create a view that returns "Hello, World!" as plain text.
2. **Post Archive** — Add a view that lists posts filtered by year using URL parameters.
3. **Search Feature** — Implement a search bar that filters posts by title using `Q` objects.
4. **Pagination** — Add pagination to the post list view (10 posts per page).
5. **User Registration** — Build a sign-up page using `UserCreationForm`.
6. **Comment System** — Create a `Comment` model linked to `Post` via a ForeignKey and display comments on the post detail page.
7. **REST API Filtering** — Add query parameter filtering to the posts API endpoint using `django-filter`.
8. **Custom Template Tag** — Write a custom template tag that displays the total number of posts.

---

## Projects

### Project 1: Personal Blog

Build a fully functional blog with:

- User registration and authentication
- CRUD operations for posts
- Comment system with moderation
- Tag-based categorization
- Pagination and search

### Project 2: Task Manager

Build a task management application with:

- User accounts with login/logout
- Create, update, and delete tasks
- Mark tasks as complete/incomplete
- Filter tasks by status
- REST API for external integrations

### Project 3: E-Commerce Store

Build a basic online store with:

- Product listing with categories
- Shopping cart stored in the session
- Order checkout flow
- Admin dashboard for managing products and orders
- REST API for product catalog

---

## Cheat Sheet

| Command | Description |
|---|---|
| `django-admin startproject <name>` | Create a new Django project |
| `python manage.py startapp <name>` | Create a new app |
| `python manage.py runserver` | Start the development server |
| `python manage.py makemigrations` | Generate migration files from model changes |
| `python manage.py migrate` | Apply migrations to the database |
| `python manage.py createsuperuser` | Create an admin superuser |
| `python manage.py collectstatic` | Collect static files for production |
| `python manage.py test` | Run tests |
| `python manage.py shell` | Open the Django interactive shell |
| `python manage.py dbshell` | Open the database shell |

### Common ORM Patterns

```python
# All objects
Model.objects.all()

# Filter
Model.objects.filter(field=value)

# Exclude
Model.objects.exclude(field=value)

# Get single object
Model.objects.get(pk=1)

# Order by
Model.objects.order_by('-created_at')

# Count
Model.objects.count()

# Exists
Model.objects.filter(field=value).exists()

# Aggregate
from django.db.models import Avg, Count, Sum
Model.objects.aggregate(Avg('price'))

# Q objects for complex queries
from django.db.models import Q
Model.objects.filter(Q(title__icontains='django') | Q(content__icontains='django'))
```

### Settings Quick Reference

```python
# Database (MySQL)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'db_name',
        'USER': 'user',
        'PASSWORD': 'password',
        'HOST': '127.0.0.1',
        'PORT': '3306',
    }
}

# Static files
STATIC_URL = '/static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'

# Media files
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'

# Authentication redirects
LOGIN_REDIRECT_URL = '/'
LOGOUT_REDIRECT_URL = '/'
```

---

## Further Reading

- [Django Official Documentation](https://docs.djangoproject.com/)
- [Django REST Framework Documentation](https://www.django-rest-framework.org/)
- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Django Girls Tutorial](https://tutorial.djangogirls.org/)
- [Two Scoops of Django (Book)](https://www.feldroy.com/books/two-scoops-of-django-3-x)
- [Classy Class-Based Views](https://ccbv.co.uk/) — Reference for all Django CBVs
- [Django Packages](https://djangopackages.org/) — Reusable apps directory
- [Mozilla Django Tutorial](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django)
