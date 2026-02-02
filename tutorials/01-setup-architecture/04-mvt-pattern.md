# The MVT Pattern Explained

## 📋 Table of Contents
- [WHY - Why MVT Architecture?](#why---why-mvt-architecture)
- [WHEN - When Does MVT Apply?](#when---when-does-mvt-apply)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why MVT Architecture?

Django uses the **MVT (Model-View-Template)** architectural pattern to separate concerns and organize code. This makes applications easier to maintain, test, and scale.

### 🎭 Real-Life Analogy: The Restaurant

Imagine a restaurant:

- **Model (Kitchen Inventory)**: Stores all the ingredients and recipes
  - What ingredients do we have?
  - How much of each ingredient?
  - Recipe instructions

- **View (Waiter)**: Takes orders and serves food
  - Takes customer requests
  - Asks kitchen for food (queries Model)
  - Brings food to customer (returns response)

- **Template (Menu)**: How food is presented
  - Menu design and layout
  - Food presentation
  - Customer-facing interface

**Request Flow:**
```
Customer → Waiter → Kitchen → Waiter → Customer
(Browser) → (View) → (Model) → (View) → (Browser)
                       ↓
                   (Template)
```

### Benefits:
- ✅ **Separation of Concerns**: Each layer has one job
- ✅ **Reusability**: Models can be used by multiple views
- ✅ **Maintainability**: Change one layer without affecting others
- ✅ **Testability**: Test each layer independently
- ✅ **Scalability**: Easy to add features

---

## 2️⃣ WHEN - When Does MVT Apply?

### MVT is Used for:
- ✅ **Every Django request**: All HTTP requests follow MVT
- ✅ **Database-driven apps**: When you need to store/retrieve data
- ✅ **Dynamic content**: Content that changes based on user/data
- ✅ **CRUD operations**: Create, Read, Update, Delete

### Exceptions (MVT not needed):
- ❌ Static files (images, CSS, JS) - served directly
- ❌ Media files - served by web server
- ❌ API responses (JSON) - View + Model (no Template)

---

## 3️⃣ HOW - Implementation

### MVT vs MVC Comparison

**MVC (Model-View-Controller)** - Traditional web frameworks:
```
Model      → Database layer
View       → Presentation layer (HTML)
Controller → Business logic
```

**MVT (Model-View-Template)** - Django:
```
Model    → Database layer (same as MVC)
View     → Business logic (MVC's Controller)
Template → Presentation layer (MVC's View)
```

**Django's "View" = MVC's "Controller"** 🤔

---

## 🏗️ MVT Components Deep Dive

### 1️⃣ MODEL - The Data Layer

**Purpose:** Define database structure and business logic

**Location:** `app/models.py`

**Example - Blog Post Model:**
```python
# blog/models.py
from django.db import models
from django.contrib.auth.models import User

class Post(models.Model):
    """
    Blog post model
    Represents a blog post in the database
    """
    # Fields define database columns
    title = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    author = models.ForeignKey(User, on_delete=models.CASCADE)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    published = models.BooleanField(default=False)
    
    class Meta:
        ordering = ['-created_at']  # Newest first
        verbose_name_plural = 'Posts'
    
    def __str__(self):
        """String representation"""
        return self.title
    
    def get_absolute_url(self):
        """Canonical URL for this post"""
        from django.urls import reverse
        return reverse('blog:post_detail', args=[self.slug])
```

**What this creates in database:**
```sql
CREATE TABLE blog_post (
    id INTEGER PRIMARY KEY,
    title VARCHAR(200),
    slug VARCHAR(50) UNIQUE,
    author_id INTEGER,
    content TEXT,
    created_at DATETIME,
    updated_at DATETIME,
    published BOOLEAN
);
```

**Model Responsibilities:**
- ✅ Define data structure
- ✅ Validate data
- ✅ Define relationships
- ✅ Business logic methods
- ✅ Database queries

---

### 2️⃣ VIEW - The Logic Layer

**Purpose:** Handle requests, process data, return responses

**Location:** `app/views.py`

**Example - Blog Post Views:**
```python
# blog/views.py
from django.shortcuts import render, get_object_or_404
from django.http import HttpResponse
from .models import Post

def post_list(request):
    """
    View: Display all published posts
    
    Flow:
    1. Receive request from user
    2. Query database for posts (Model)
    3. Pass data to template (Template)
    4. Return rendered HTML (Response)
    """
    # Step 1: Get data from Model
    posts = Post.objects.filter(published=True)
    
    # Step 2: Prepare context (data for template)
    context = {
        'posts': posts,
        'page_title': 'Blog Posts',
    }
    
    # Step 3: Render template with context
    return render(request, 'blog/post_list.html', context)


def post_detail(request, slug):
    """
    View: Display single post
    
    Args:
        request: HTTP request object
        slug: Post slug from URL
    """
    # Get post or return 404
    post = get_object_or_404(Post, slug=slug, published=True)
    
    context = {
        'post': post,
    }
    
    return render(request, 'blog/post_detail.html', context)


def hello_world(request):
    """
    Simplest view - no Model or Template
    """
    return HttpResponse("<h1>Hello, World!</h1>")
```

**View Responsibilities:**
- ✅ Receive HTTP requests
- ✅ Query database (via Models)
- ✅ Process business logic
- ✅ Prepare context data
- ✅ Render templates
- ✅ Return HTTP responses

---

### 3️⃣ TEMPLATE - The Presentation Layer

**Purpose:** Define HTML structure and display data

**Location:** `app/templates/app/template.html`

**Example - Blog Post Template:**
```html
<!-- blog/templates/blog/post_list.html -->
<!DOCTYPE html>
<html>
<head>
    <title>{{ page_title }}</title>
</head>
<body>
    <h1>{{ page_title }}</h1>
    
    {% if posts %}
        <!-- Loop through posts -->
        {% for post in posts %}
            <article>
                <h2>
                    <a href="{% url 'blog:post_detail' post.slug %}">
                        {{ post.title }}
                    </a>
                </h2>
                <p class="meta">
                    By {{ post.author.username }} on {{ post.created_at|date:"F d, Y" }}
                </p>
                <p>{{ post.content|truncatewords:30 }}</p>
            </article>
            <hr>
        {% endfor %}
    {% else %}
        <p>No posts available.</p>
    {% endif %}
</body>
</html>
```

**Template Features Used:**
- `{{ variable }}` - Display variable
- `{% for %}` - Loop through items
- `{% if %}` - Conditional logic
- `{% url %}` - Generate URLs
- `|filter` - Transform data (date, truncate)

**Template Responsibilities:**
- ✅ Display data from view
- ✅ HTML structure
- ✅ Template inheritance
- ✅ Basic logic (loops, conditionals)
- ✅ Filters for data formatting

---

## 🔄 Complete MVT Request Flow

### Scenario: User visits `/blog/django-tutorial/`

#### Step 1: URL Routing
```python
# mysite/urls.py
from django.urls import path, include

urlpatterns = [
    path('blog/', include('blog.urls')),
]

# blog/urls.py
from django.urls import path
from . import views

app_name = 'blog'
urlpatterns = [
    path('<slug:slug>/', views.post_detail, name='post_detail'),
]
```

#### Step 2: View Processes Request
```python
# blog/views.py
def post_detail(request, slug):
    # Query Model
    post = Post.objects.get(slug=slug)
    
    # Prepare context
    context = {'post': post}
    
    # Render template
    return render(request, 'blog/post_detail.html', context)
```

#### Step 3: Model Returns Data
```python
# blog/models.py
class Post(models.Model):
    title = models.CharField(max_length=200)
    # ... other fields
```

#### Step 4: Template Renders HTML
```html
<!-- blog/templates/blog/post_detail.html -->
<h1>{{ post.title }}</h1>
<p>{{ post.content }}</p>
```

#### Step 5: Response Sent to Browser
```html
<h1>Django Tutorial</h1>
<p>Learn Django from scratch...</p>
```

**Complete Flow Diagram:**
```
User Request: /blog/django-tutorial/
    ↓
URL Dispatcher (urls.py)
    ↓
View Function (views.py)
    ↓
Model Query (models.py) → Database
    ↓
Template Rendering (template.html)
    ↓
HTTP Response → User Browser
```

---

## 🎯 Practical Example: Todo App

### 1. Model (Data)
```python
# todos/models.py
from django.db import models

class Task(models.Model):
    title = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    completed = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.title
```

### 2. View (Logic)
```python
# todos/views.py
from django.shortcuts import render, redirect
from .models import Task

def task_list(request):
    """Display all tasks"""
    tasks = Task.objects.all().order_by('-created_at')
    return render(request, 'todos/task_list.html', {'tasks': tasks})

def task_create(request):
    """Create new task"""
    if request.method == 'POST':
        title = request.POST.get('title')
        description = request.POST.get('description')
        Task.objects.create(title=title, description=description)
        return redirect('task_list')
    return render(request, 'todos/task_form.html')

def task_toggle(request, task_id):
    """Toggle task completion"""
    task = Task.objects.get(id=task_id)
    task.completed = not task.completed
    task.save()
    return redirect('task_list')
```

### 3. Template (Presentation)
```html
<!-- todos/templates/todos/task_list.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Todo List</title>
</head>
<body>
    <h1>My Tasks</h1>
    
    <a href="{% url 'task_create' %}">Add New Task</a>
    
    <ul>
        {% for task in tasks %}
            <li>
                <input type="checkbox" 
                       {% if task.completed %}checked{% endif %}
                       onclick="location.href='{% url 'task_toggle' task.id %}'">
                <span {% if task.completed %}style="text-decoration: line-through"{% endif %}>
                    {{ task.title }}
                </span>
                <small>{{ task.created_at|date:"M d, Y" }}</small>
            </li>
        {% empty %}
            <li>No tasks yet!</li>
        {% endfor %}
    </ul>
</body>
</html>
```

### 4. URLs (Routing)
```python
# todos/urls.py
from django.urls import path
from . import views

urlpatterns = [
    path('', views.task_list, name='task_list'),
    path('create/', views.task_create, name='task_create'),
    path('toggle/<int:task_id>/', views.task_toggle, name='task_toggle'),
]
```

**Result:**
```
GET  /todos/              → Show all tasks
GET  /todos/create/       → Show form
POST /todos/create/       → Create task
GET  /todos/toggle/1/     → Toggle task #1
```

---

## 💡 MVT Best Practices

### ✅ Models - DO:
1. **Business logic in models**: Keep logic with data
2. **Use meaningful names**: `Post`, `Task`, not `Data1`
3. **Add __str__ methods**: For readability
4. **Use validators**: Ensure data integrity
5. **Document fields**: Add help_text

### ✅ Views - DO:
1. **Keep views thin**: Minimal logic
2. **Use shortcuts**: `render()`, `get_object_or_404()`
3. **Handle errors**: Try/except blocks
4. **Validate input**: Check POST data
5. **Use decorators**: `@login_required`, etc.

### ✅ Templates - DO:
1. **Separate logic**: No complex Python
2. **Use template inheritance**: DRY principle
3. **Use filters**: Format data in templates
4. **Keep simple**: If complex, move to view
5. **Use template tags**: Built-in tools

### ❌ DON'T:
1. **Don't put HTML in views**: Use templates
2. **Don't put logic in templates**: Use views
3. **Don't duplicate code**: Use inheritance
4. **Don't skip validation**: Always validate
5. **Don't hardcode URLs**: Use `{% url %}`

---

## ✏️ Practice Exercise

### Exercise 4.1: Build a Contact Form

**Task:** Create a complete MVT implementation for a contact form.

**Requirements:**
1. **Model**: `Contact` with name, email, message, created_at
2. **View**: Display form and save submissions
3. **Template**: Form with Bootstrap styling
4. **URL**: `/contact/` and `/contact/success/`

**Starter Code:**

```python
# contacts/models.py
from django.db import models

class Contact(models.Model):
    # TODO: Add fields
    pass
```

```python
# contacts/views.py
from django.shortcuts import render, redirect
from .models import Contact

def contact_form(request):
    # TODO: Handle GET and POST
    pass

def contact_success(request):
    # TODO: Show success message
    pass
```

```html
<!-- contacts/templates/contacts/form.html -->
<!-- TODO: Create form -->
```

---

### Exercise 4.2: Diagram MVT Flow

**Task:** Draw a flowchart showing MVT for this scenario:

**User Action:** Submit product review

**Steps to diagram:**
1. User submits form
2. URL routes to view
3. View validates data
4. Model saves to database
5. View redirects to product page
6. Template displays updated reviews

**Create:** `mvt_flow.md` with ASCII diagram

---

### Exercise 4.3: Identify MVT Violations

**Find the problems in this code:**

```python
# BAD EXAMPLE - Don't do this!

# views.py
def bad_view(request):
    # Problem 1: HTML in view
    html = "<h1>Products</h1><ul>"
    
    # Problem 2: Direct SQL
    cursor = connection.cursor()
    cursor.execute("SELECT * FROM products")
    
    for row in cursor:
        html += f"<li>{row[1]}</li>"
    
    html += "</ul>"
    return HttpResponse(html)

# template.html
<!-- Problem 3: Business logic in template -->
{% for product in products %}
    {% if product.price > 100 %}
        {% load calculate_discount %}
        {{ product.price|complex_calculation:product.category }}
    {% endif %}
{% endfor %}

# models.py
class Product(models.Model):
    name = models.CharField(max_length=200)
    # Problem 4: No __str__, no Meta, no methods
```

**Your Task:** Fix this code following MVT principles.

---

## 🎓 Key Takeaways

1. ✅ MVT = Model (Data) + View (Logic) + Template (Presentation)
2. ✅ Models define database structure and business logic
3. ✅ Views handle requests and prepare data
4. ✅ Templates render HTML with data
5. ✅ Each layer has a specific responsibility - don't mix them!

---

## 🔗 Additional Resources

- [Django MVT documentation](https://docs.djangoproject.com/en/4.2/faq/general/#django-appears-to-be-a-mvc-framework-but-you-call-the-controller-the-view-and-the-view-the-template-how-come-you-don-t-use-the-standard-names)
- [MVT vs MVC](https://www.geeksforgeeks.org/difference-between-mvc-and-mvt-design-patterns/)
- [Django design philosophies](https://docs.djangoproject.com/en/4.2/misc/design-philosophies/)

---

## 📚 Next Steps

Let's configure Django settings for development and production!

[← Previous: Project vs App](./03-project-vs-app.md) | [Next: Settings & Configuration →](./05-settings-configuration.md)
