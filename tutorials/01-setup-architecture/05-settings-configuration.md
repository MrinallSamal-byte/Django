# Settings & Configuration

## 📋 Table of Contents
- [WHY - Why Configure Settings?](#why---why-configure-settings)
- [WHEN - When to Modify Settings?](#when---when-to-modify-settings)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Configure Settings?

Django's `settings.py` is the central configuration file for your project. It controls everything from database connections to security settings, making your app customizable for different environments (development, staging, production).

### 🎭 Real-Life Analogy: The Control Panel
Think of settings.py as your car's dashboard:
- **DEBUG mode**: Test mode (check engine light on)
- **DATABASES**: Fuel type (diesel vs gasoline)
- **ALLOWED_HOSTS**: Authorized drivers
- **SECRET_KEY**: Car key (unique security)
- **INSTALLED_APPS**: Car features (GPS, AC, radio)

### Benefits:
- ✅ **Centralized Config**: One file for all settings
- ✅ **Environment-Specific**: Dev vs Production
- ✅ **Security**: Manage secrets properly
- ✅ **Flexibility**: Easy to customize behavior
- ✅ **Scalability**: Add features without code changes

---

## 2️⃣ WHEN - When to Modify Settings?

### Modify Settings When:
- ✅ Adding new apps
- ✅ Changing database
- ✅ Configuring static/media files
- ✅ Setting up authentication
- ✅ Deploying to production
- ✅ Adding middleware
- ✅ Configuring internationalization

### Don't Modify When:
- ❌ Just learning (use defaults)
- ❌ Unsure about security impact
- ❌ Without reading documentation

---

## 3️⃣ HOW - Implementation

## 📄 Understanding settings.py

### Default Structure
```python
# mysite/settings.py
import os
from pathlib import Path

# Build paths inside the project
BASE_DIR = Path(__file__).resolve().parent.parent

# SECURITY WARNING: keep the secret key used in production secret!
SECRET_KEY = 'django-insecure-...'

# SECURITY WARNING: don't run with debug turned on in production!
DEBUG = True

ALLOWED_HOSTS = []

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
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

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'mysite.wsgi.application'

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator'},
    {'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator'},
    {'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator'},
    {'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator'},
]

# Internationalization
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_TZ = True

# Static files (CSS, JavaScript, Images)
STATIC_URL = 'static/'

# Default primary key field type
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'
```

---

## 🔑 Essential Settings Explained

### 1. BASE_DIR
```python
BASE_DIR = Path(__file__).resolve().parent.parent
```

**Purpose:** Root directory of your project
**Usage:**
```python
DATABASES = {
    'default': {
        'NAME': BASE_DIR / 'db.sqlite3',  # Uses BASE_DIR
    }
}

TEMPLATES = [
    {
        'DIRS': [BASE_DIR / 'templates'],  # Global templates
    }
]
```

---

### 2. SECRET_KEY
```python
SECRET_KEY = 'django-insecure-abc123...'
```

**Purpose:** Cryptographic signing key
**Used for:**
- Session encryption
- CSRF tokens
- Password reset tokens
- Signing cookies

**⚠️ NEVER commit to Git!**

**Best Practice:**
```python
# settings.py
import os
SECRET_KEY = os.environ.get('SECRET_KEY', 'dev-key-only')

# .env file (not in Git)
SECRET_KEY=your-production-secret-key-here
```

---

### 3. DEBUG
```python
DEBUG = True  # Development
DEBUG = False  # Production
```

**When DEBUG = True:**
- ✅ Detailed error pages
- ✅ Auto-reload on code changes
- ✅ Shows SQL queries
- ❌ Exposes sensitive data

**When DEBUG = False:**
- ✅ Hides errors from users
- ✅ Serves static files differently
- ❌ Requires ALLOWED_HOSTS

**Best Practice:**
```python
DEBUG = os.environ.get('DEBUG', 'False') == 'True'
```

---

### 4. ALLOWED_HOSTS
```python
ALLOWED_HOSTS = []  # Development (DEBUG=True)
ALLOWED_HOSTS = ['mysite.com', 'www.mysite.com']  # Production
```

**Purpose:** Host/domain names Django can serve
**Required when:** DEBUG = False

**Examples:**
```python
# Development
ALLOWED_HOSTS = ['localhost', '127.0.0.1']

# Production
ALLOWED_HOSTS = [
    'mysite.com',
    'www.mysite.com',
    '192.168.1.100',
]

# Allow all (DANGEROUS - testing only)
ALLOWED_HOSTS = ['*']
```

---

### 5. INSTALLED_APPS
```python
INSTALLED_APPS = [
    # Django apps
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    
    # Third-party apps
    'rest_framework',
    'crispy_forms',
    
    # Your apps
    'blog',
    'products',
    'users',
]
```

**Order matters:**
1. Django contrib apps (admin, auth, etc.)
2. Third-party apps
3. Your custom apps

---

### 6. MIDDLEWARE
```python
MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',          # Security headers
    'django.contrib.sessions.middleware.SessionMiddleware',   # Session management
    'django.middleware.common.CommonMiddleware',              # Common functionality
    'django.middleware.csrf.CsrfViewMiddleware',             # CSRF protection
    'django.contrib.auth.middleware.AuthenticationMiddleware', # Authentication
    'django.contrib.messages.middleware.MessageMiddleware',   # Flash messages
    'django.middleware.clickjacking.XFrameOptionsMiddleware', # Clickjacking protection
]
```

**Purpose:** Process requests/responses globally
**Order matters:** Top to bottom on request, bottom to top on response

---

### 7. DATABASES
```python
# SQLite (default)
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# PostgreSQL
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '5432',
    }
}

# MySQL
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mydatabase',
        'USER': 'mydatabaseuser',
        'PASSWORD': 'mypassword',
        'HOST': 'localhost',
        'PORT': '3306',
    }
}
```

---

### 8. TEMPLATES
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],  # Global templates directory
        'APP_DIRS': True,  # Look for templates in each app
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
```

---

### 9. STATIC_URL & STATIC_ROOT
```python
# Development
STATIC_URL = '/static/'
STATICFILES_DIRS = [BASE_DIR / 'static']

# Production (after collectstatic)
STATIC_ROOT = BASE_DIR / 'staticfiles'
```

**Usage in templates:**
```html
{% load static %}
<link rel="stylesheet" href="{% static 'css/style.css' %}">
<img src="{% static 'images/logo.png' %}">
```

---

### 10. MEDIA Settings
```python
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'
```

**Purpose:** User-uploaded files (images, documents)

**Configure URLs (development):**
```python
# mysite/urls.py
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... your patterns
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

---

## 🎯 Environment-Specific Settings

### Development Settings
```python
# settings/development.py
from .base import *

DEBUG = True
ALLOWED_HOSTS = ['localhost', '127.0.0.1']

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': BASE_DIR / 'db.sqlite3',
    }
}

# Show emails in console
EMAIL_BACKEND = 'django.core.mail.backends.console.EmailBackend'
```

---

### Production Settings
```python
# settings/production.py
from .base import *
import os

DEBUG = False
ALLOWED_HOSTS = ['mysite.com', 'www.mysite.com']

SECRET_KEY = os.environ.get('SECRET_KEY')

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME'),
        'USER': os.environ.get('DB_USER'),
        'PASSWORD': os.environ.get('DB_PASSWORD'),
        'HOST': os.environ.get('DB_HOST'),
        'PORT': '5432',
    }
}

# Security settings
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
```

---

### Using Environment Variables
```python
# settings.py
import os
from pathlib import Path

# Load environment variables
from dotenv import load_dotenv
load_dotenv()

SECRET_KEY = os.environ.get('SECRET_KEY')
DEBUG = os.environ.get('DEBUG', 'False') == 'True'

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.environ.get('DB_NAME', 'mydb'),
        'USER': os.environ.get('DB_USER', 'postgres'),
        'PASSWORD': os.environ.get('DB_PASSWORD', ''),
        'HOST': os.environ.get('DB_HOST', 'localhost'),
        'PORT': os.environ.get('DB_PORT', '5432'),
    }
}
```

**.env file (DO NOT COMMIT):**
```env
SECRET_KEY=your-secret-key-here
DEBUG=True
DB_NAME=mydatabase
DB_USER=myuser
DB_PASSWORD=mypassword
DB_HOST=localhost
DB_PORT=5432
```

**Install python-dotenv:**
```bash
pip install python-dotenv
```

---

## 🔒 Security Settings

### Essential Security Headers
```python
# Production only
if not DEBUG:
    SECURE_SSL_REDIRECT = True
    SESSION_COOKIE_SECURE = True
    CSRF_COOKIE_SECURE = True
    SECURE_BROWSER_XSS_FILTER = True
    SECURE_CONTENT_TYPE_NOSNIFF = True
    X_FRAME_OPTIONS = 'DENY'
    SECURE_HSTS_SECONDS = 31536000
    SECURE_HSTS_INCLUDE_SUBDOMAINS = True
    SECURE_HSTS_PRELOAD = True
```

---

## 🌍 Internationalization Settings
```python
LANGUAGE_CODE = 'en-us'  # Default language
TIME_ZONE = 'America/New_York'  # Your timezone
USE_I18N = True  # Enable internationalization
USE_L10N = True  # Enable localization
USE_TZ = True    # Use timezone-aware datetimes

# Multiple languages
LANGUAGES = [
    ('en', 'English'),
    ('es', 'Spanish'),
    ('fr', 'French'),
]
```

---

## ✏️ Practice Exercise

### Exercise 5.1: Configure Multiple Environments

**Task:** Set up separate settings for development and production.

**Structure:**
```
mysite/
└── mysite/
    └── settings/
        ├── __init__.py
        ├── base.py       # Common settings
        ├── development.py # Dev-specific
        └── production.py  # Prod-specific
```

**base.py:**
```python
# Common settings for all environments
from pathlib import Path

BASE_DIR = Path(__file__).resolve().parent.parent.parent

INSTALLED_APPS = [
    # ... apps
]
# ... other common settings
```

**development.py:**
```python
from .base import *

DEBUG = True
ALLOWED_HOSTS = ['localhost']
# ... dev settings
```

**Run with specific settings:**
```bash
# Development
python manage.py runserver --settings=mysite.settings.development

# Production
python manage.py runserver --settings=mysite.settings.production
```

---

### Exercise 5.2: Use Environment Variables

**Task:** Create a `.env` file and load secrets.

**Requirements:**
1. Install `python-dotenv`
2. Create `.env` file with secrets
3. Update settings.py to use environment variables
4. Add `.env` to `.gitignore`

**.env:**
```env
SECRET_KEY=my-secret-key-12345
DEBUG=True
DATABASE_URL=sqlite:///db.sqlite3
ALLOWED_HOSTS=localhost,127.0.0.1
```

**settings.py:**
```python
from dotenv import load_dotenv
import os

load_dotenv()

SECRET_KEY = os.environ.get('SECRET_KEY')
DEBUG = os.environ.get('DEBUG') == 'True'
```

---

### Exercise 5.3: Security Checklist

**Task:** Run Django's security check and fix issues.

```bash
python manage.py check --deploy
```

**Fix all warnings for:**
- SECRET_KEY not set
- DEBUG = True in production
- ALLOWED_HOSTS not set
- Missing security headers
- Insecure cookies

---

## 🎓 Key Takeaways

1. ✅ `settings.py` controls all Django configuration
2. ✅ Use environment variables for secrets
3. ✅ Separate dev and production settings
4. ✅ Never commit SECRET_KEY or passwords
5. ✅ Run security checks before deployment

---

## 🔗 Additional Resources

- [Django settings documentation](https://docs.djangoproject.com/en/4.2/ref/settings/)
- [Deployment checklist](https://docs.djangoproject.com/en/4.2/howto/deployment/checklist/)
- [Environment variables](https://django-environ.readthedocs.io/)

---

## 📚 Next Steps

Congratulations! You've completed Part 1: Setup & Architecture. Now let's dive into Data Modeling!

[← Previous: MVT Pattern](./04-mvt-pattern.md) | [Next: Part 2 - Data Modeling →](../02-data-modeling/README.md)
