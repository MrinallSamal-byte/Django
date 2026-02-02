# Django-Admin & Project Creation

## 📋 Table of Contents
- [WHY - Why Use django-admin?](#why---why-use-django-admin)
- [WHEN - When to Use django-admin?](#when---when-to-use-django-admin)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use django-admin?

`django-admin` is Django's command-line utility that automates common development tasks. It generates boilerplate code, runs the development server, manages database migrations, and much more.

### 🎭 Real-Life Analogy: The Construction Foreman
Think of `django-admin` as a construction foreman who:
- Sets up the building foundation (startproject)
- Creates new rooms (startapp)
- Handles blueprints (migrations)
- Starts/stops utilities (runserver)

Without it, you'd have to manually create dozens of files and configurations!

### Benefits:
- ✅ **Rapid Setup**: Creates project structure in seconds
- ✅ **Consistency**: Standard Django project layout
- ✅ **Best Practices**: Built-in security and configuration
- ✅ **Time-Saving**: No manual boilerplate coding
- ✅ **Error Prevention**: Correct directory structure guaranteed

---

## 2️⃣ WHEN - When to Use django-admin?

### Use django-admin for:
- ✅ Creating a new Django project (`startproject`)
- ✅ Creating new apps (`startapp`)
- ✅ Running management commands (initial setup)

### Use manage.py for:
- ✅ All other commands (after project creation)
- ✅ Running the development server
- ✅ Database migrations
- ✅ Creating superusers

**Key Difference:**
- `django-admin`: Works anywhere, no Django project needed
- `manage.py`: Project-specific, uses your settings

---

## 3️⃣ HOW - Implementation

### Step 1: Verify Django Installation

```bash
# Activate your virtual environment first!
source venv/bin/activate  # Windows: venv\Scripts\activate

# Check django-admin is available
django-admin --version
```

**Expected Output:**
```
4.2.7
```

---

### Step 2: Create Your First Django Project

```bash
# Basic syntax
django-admin startproject project_name

# Example: Create a project named 'mysite'
django-admin startproject mysite
```

**What Django creates:**
```
mysite/                     # Project root directory
├── manage.py              # Command-line utility (project-specific)
└── mysite/                # Python package for your project
    ├── __init__.py        # Makes it a Python package
    ├── settings.py        # Project settings/configuration
    ├── urls.py            # URL declarations (routing)
    ├── asgi.py            # ASGI server entry point
    └── wsgi.py            # WSGI server entry point
```

---

### Step 3: Understand the Generated Files

#### 📄 manage.py
```python
#!/usr/bin/env python
"""Django's command-line utility for administrative tasks."""
import os
import sys

def main():
    """Run administrative tasks."""
    os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
    # ... more code
```

**Purpose:** Project-specific wrapper around `django-admin`
- Sets the `DJANGO_SETTINGS_MODULE` environment variable
- Provides a single command interface for your project

---

#### 📄 \_\_init\_\_.py
```python
# Empty file
```

**Purpose:** Tells Python this directory is a package
- Allows imports like `from mysite.settings import DEBUG`
- Required for Python package structure

---

#### 📄 settings.py (excerpt)
```python
# Quick-start development settings
SECRET_KEY = 'django-insecure-...'  # Auto-generated secret key
DEBUG = True                         # Development mode
ALLOWED_HOSTS = []                   # Hosts allowed to serve the app

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',          # Admin interface
    'django.contrib.auth',           # Authentication
    'django.contrib.contenttypes',   # Content types framework
    'django.contrib.sessions',       # Session management
    'django.contrib.messages',       # Messaging framework
    'django.contrib.staticfiles',    # Static file management
]

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# ... more settings
```

**Purpose:** Central configuration for your Django project
- Database settings
- Installed apps
- Middleware configuration
- Templates, static files, etc.

---

#### 📄 urls.py
```python
from django.contrib import admin
from django.urls import path

urlpatterns = [
    path('admin/', admin.site.urls),
]
```

**Purpose:** URL routing configuration
- Maps URLs to views
- Includes app-specific URLs
- Default admin route included

---

#### 📄 wsgi.py & asgi.py
```python
# wsgi.py - Web Server Gateway Interface
import os
from django.core.wsgi import get_wsgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
application = get_wsgi_application()
```

```python
# asgi.py - Asynchronous Server Gateway Interface
import os
from django.core.asgi import get_asgi_application

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'mysite.settings')
application = get_asgi_application()
```

**Purpose:** Deployment interfaces
- **WSGI**: Synchronous deployments (Gunicorn, uWSGI)
- **ASGI**: Asynchronous deployments (Daphne, Uvicorn)
- Usually don't need to modify these

---

### Step 4: Run the Development Server

```bash
# Navigate into the project directory
cd mysite

# Run the development server
python manage.py runserver
```

**Terminal Output:**
```
Watching for file changes with StatReloader
Performing system checks...

System check identified no issues (0 silenced).

You have 18 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.

December 02, 2023 - 15:30:45
Django version 4.2.7, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```

---

### Step 5: Visit Your Django Site

Open your browser and navigate to:
```
http://127.0.0.1:8000/
```

You should see the Django welcome page! 🎉

**What you'll see:**
```
The install worked successfully! Congratulations!

You are seeing this page because DEBUG=True is in your settings file 
and you have not configured any URLs.
```

---

### Step 6: Access the Admin Interface

```
http://127.0.0.1:8000/admin/
```

You'll see a login page (we'll create a superuser later).

---

## 🎯 Complete Project Creation Workflow

```bash
# 1. Ensure virtual environment is activated
source venv/bin/activate

# 2. Create the project
django-admin startproject myshop

# 3. Navigate into project
cd myshop

# 4. Apply initial migrations
python manage.py migrate

# 5. Create a superuser
python manage.py createsuperuser

# 6. Run the development server
python manage.py runserver
```

**Interactive superuser creation:**
```
Username: admin
Email address: admin@example.com
Password: ********
Password (again): ********
Superuser created successfully.
```

---

## 📂 Alternative Project Structures

### Option 1: Dot Notation (Current Directory)
```bash
# Creates project in current directory (no extra folder)
django-admin startproject mysite .
```

**Result:**
```
current_directory/
├── manage.py
└── mysite/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

### Option 2: Custom Template
```bash
# Use a custom project template
django-admin startproject mysite --template=/path/to/template
```

---

## 🔧 Common django-admin Commands

### Project Management
```bash
# Create new project
django-admin startproject project_name

# Create new app (after project creation)
django-admin startapp app_name

# Check Django version
django-admin --version

# Get help
django-admin help
django-admin help startproject
```

### manage.py Commands (Use After Project Creation)
```bash
# Run development server
python manage.py runserver
python manage.py runserver 8080         # Custom port
python manage.py runserver 0.0.0.0:8000 # All network interfaces

# Database operations
python manage.py migrate                 # Apply migrations
python manage.py makemigrations          # Create migrations
python manage.py showmigrations          # Show migration status

# User management
python manage.py createsuperuser         # Create admin user
python manage.py changepassword username # Change user password

# Shell and utilities
python manage.py shell                   # Python shell with Django
python manage.py dbshell                 # Database shell
python manage.py check                   # Check for problems

# Static files
python manage.py collectstatic           # Collect static files
```

---

## 🎯 Practical Examples

### Example 1: Blog Project
```bash
# Create project
django-admin startproject myblog

# Structure created
myblog/
├── manage.py
└── myblog/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py

# Start server
cd myblog
python manage.py migrate
python manage.py runserver
```

---

### Example 2: E-commerce Project
```bash
# Create in current directory
mkdir shop_project
cd shop_project
django-admin startproject config .

# Structure created (cleaner)
shop_project/
├── manage.py
└── config/
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    ├── asgi.py
    └── wsgi.py
```

---

## 🐛 Common Issues & Solutions

### Issue 1: "django-admin: command not found"
**Cause:** Virtual environment not activated or Django not installed

**Solution:**
```bash
# Activate virtual environment
source venv/bin/activate

# Install Django
pip install django

# Verify
django-admin --version
```

---

### Issue 2: Project Name Conflicts
```bash
# ❌ DON'T use Python module names
django-admin startproject test  # Conflicts with 'test' module
django-admin startproject django  # Conflicts with Django itself
```

**Solution:**
```bash
# ✅ Use descriptive, unique names
django-admin startproject blog_project
django-admin startproject my_ecommerce_site
```

---

### Issue 3: "Port already in use"
```
Error: That port is already in use.
```

**Solution:**
```bash
# Use a different port
python manage.py runserver 8080

# Or kill the process using port 8000
# Windows: netstat -ano | findstr :8000
# Linux/Mac: lsof -ti:8000 | xargs kill -9
```

---

### Issue 4: Permission Errors
**Solution:**
```bash
# Don't use sudo! Use virtual environment instead
# ❌ sudo django-admin startproject mysite
# ✅ django-admin startproject mysite
```

---

## 💡 Best Practices

### ✅ DO:
1. **Use meaningful names**: `blog_project`, `ecommerce_site`
2. **Activate venv first**: Always work in virtual environment
3. **Use manage.py**: After project creation, use `manage.py` not `django-admin`
4. **Run migrate early**: Apply initial migrations immediately
5. **Create superuser**: Set up admin access right away

### ❌ DON'T:
1. **Don't use reserved names**: Avoid `django`, `test`, `site`
2. **Don't nest projects**: One Django project per directory
3. **Don't modify core files**: Don't edit `wsgi.py`, `asgi.py` unless necessary
4. **Don't commit SECRET_KEY**: Use environment variables (we'll cover this)
5. **Don't run as root**: Always use virtual environment

---

## ✏️ Practice Exercise

### Exercise 2.1: Create Your First Project

**Task:** Create a Django project for a personal portfolio website.

**Requirements:**
1. Project name: `portfolio_site`
2. Apply initial migrations
3. Create a superuser (username: `admin`, email: your email)
4. Run development server on port 8080
5. Access admin interface and login

**Expected Steps:**
```bash
django-admin startproject portfolio_site
cd portfolio_site
python manage.py migrate
python manage.py createsuperuser
python manage.py runserver 8080
# Visit: http://127.0.0.1:8080/admin/
```

---

### Exercise 2.2: Explore Project Structure

**Task:** Document what each file does in your created project.

**Create a file:** `project_structure.md`

**Content should include:**
```markdown
# Portfolio Site Structure

## manage.py
- Purpose: [Your explanation]
- Used for: [Your explanation]

## settings.py
- Contains: [Your explanation]
- Important settings: [Your list]

## urls.py
- Purpose: [Your explanation]
- Default routes: [Your explanation]
```

---

### Exercise 2.3: Multiple Projects

**Task:** Create three separate Django projects in the same parent directory:

1. **blog_project** - Personal blog
2. **todo_app** - Task manager
3. **api_service** - REST API

**Directory structure should be:**
```
django_projects/
├── blog_project/
│   ├── manage.py
│   └── blog_project/
├── todo_app/
│   ├── manage.py
│   └── todo_app/
└── api_service/
    ├── manage.py
    └── api_service/
```

**Bonus:** Run all three on different ports simultaneously:
- Blog: 8000
- Todo: 8001
- API: 8002

---

## 🎓 Key Takeaways

1. ✅ `django-admin startproject` creates a new Django project
2. ✅ Generated project includes essential files: settings.py, urls.py, manage.py
3. ✅ Use `manage.py` for all commands after project creation
4. ✅ Run `python manage.py migrate` before starting development
5. ✅ Create a superuser to access the admin interface

---

## 🔗 Additional Resources

- [Django-admin documentation](https://docs.djangoproject.com/en/4.2/ref/django-admin/)
- [manage.py commands](https://docs.djangoproject.com/en/4.2/ref/django-admin/)
- [Project structure best practices](https://docs.djangoproject.com/en/4.2/intro/tutorial01/)

---

## 📚 Next Steps

Now that you have a Django project, let's understand the difference between projects and apps!

[← Previous: Virtual Environments](./01-virtual-environments.md) | [Next: Project vs App Structure →](./03-project-vs-app.md)
