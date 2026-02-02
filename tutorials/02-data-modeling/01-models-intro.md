# Introduction to Django Models

## 📋 Table of Contents
- [WHY - Why Use Django Models?](#why---why-use-django-models)
- [WHEN - When to Use Models?](#when---when-to-use-models)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use Django Models?

Django models are Python classes that represent database tables. They provide an object-oriented way to interact with your database without writing SQL. This is called ORM (Object-Relational Mapping).

### 🎭 Real-Life Analogy: The Product Catalog

Imagine you run an online store with a product catalog:
- **Without Models (Raw SQL)**: You write complex SQL queries every time you need to add, update, or retrieve products. It's like manually writing inventory cards for each product.
- **With Models**: You define a Product class once, and Django handles all database operations. It's like having an automated inventory management system!

### Benefits of Django Models:

- ✅ **No SQL Required**: Write Python code instead of SQL queries
- ✅ **Database Agnostic**: Switch databases (SQLite, PostgreSQL, MySQL) without changing code
- ✅ **Type Safety**: Python helps catch errors before they reach the database
- ✅ **Built-in Validation**: Automatic data validation before saving
- ✅ **Relationships**: Easy to define relationships between tables
- ✅ **Migration Management**: Automatic database schema version control
- ✅ **Admin Interface**: Free admin panel for data management

### The ORM Concept:

```
Python Class (Model)  ←→  Database Table
Class Attribute       ←→  Table Column
Class Instance        ←→  Table Row
```

**Example:**
```python
# Python Model
class Product:
    name = models.CharField(max_length=100)
    price = models.DecimalField(max_digits=10, decimal_places=2)

# Creates SQL Table:
# CREATE TABLE product (
#     id INTEGER PRIMARY KEY,
#     name VARCHAR(100),
#     price DECIMAL(10, 2)
# );
```

---

## 2️⃣ WHEN - When to Use Models?

### ✅ Always Use Models When:

- Storing data that needs to persist (products, users, orders, etc.)
- You need CRUD operations (Create, Read, Update, Delete)
- Building any database-driven application
- You want database relationships (one-to-many, many-to-many)
- You need data validation and integrity

### Common Use Cases:

1. **E-commerce**: Products, orders, customers, shopping carts
2. **Blog**: Posts, comments, categories, tags
3. **Social Media**: Users, posts, likes, follows
4. **Content Management**: Articles, pages, media files
5. **Business Apps**: Employees, departments, projects, tasks

### ❌ Don't Use Models For:

- Temporary data that doesn't need to persist (use Python variables)
- Cache data (use Django's cache framework)
- Session data (use Django's session framework)

---

## 3️⃣ HOW - Implementation

### Step 1: Create a Django App

Models live inside Django apps. First, create an app:

```bash
# Create an app called 'products'
python manage.py startapp products
```

**Directory Structure:**
```
products/
├── __init__.py
├── admin.py          # Register models for admin
├── apps.py
├── models.py         # Define models here ← We'll work here
├── tests.py
└── views.py
```

### Step 2: Register the App

Add the app to `settings.py`:

```python
# myproject/settings.py

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'products',  # ← Add your app here
]
```

---

### Step 3: Define Your First Model

Open `products/models.py`:

```python
from django.db import models

# Every model inherits from models.Model
class Product(models.Model):
    """
    Represents a product in our store.
    This will create a 'products_product' table in the database.
    """
    # CharField for short text (required: max_length)
    name = models.CharField(max_length=200)
    
    # TextField for long text (unlimited length)
    description = models.TextField()
    
    # DecimalField for prices (precise decimal numbers)
    price = models.DecimalField(
        max_digits=10,  # Total digits (including decimals)
        decimal_places=2  # Digits after decimal point
    )
    
    # IntegerField for whole numbers
    stock_quantity = models.IntegerField(default=0)
    
    # BooleanField for True/False values
    is_active = models.BooleanField(default=True)
    
    # DateTimeField for timestamps (auto_now_add sets on creation)
    created_at = models.DateTimeField(auto_now_add=True)
    
    # DateTimeField (auto_now updates on every save)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        """
        String representation of the model.
        Shows in admin panel and when printing the object.
        """
        return self.name
    
    class Meta:
        """
        Metadata for the model.
        """
        ordering = ['-created_at']  # Order by newest first
        verbose_name = 'Product'
        verbose_name_plural = 'Products'
```

**What Each Part Does:**

1. **`class Product(models.Model)`**: Defines a model that Django will convert to a database table
2. **Fields**: Each class attribute becomes a database column
3. **`__str__` method**: Returns a human-readable representation
4. **`Meta` class**: Provides metadata like ordering and naming

---

### Step 4: Create the Database Table

Run these commands to create the table:

```bash
# 1. Create migration files (instructions for database changes)
python manage.py makemigrations

# Output:
# Migrations for 'products':
#   products/migrations/0001_initial.py
#     - Create model Product

# 2. Apply migrations (execute the changes)
python manage.py migrate

# Output:
# Operations to perform:
#   Apply all migrations: admin, auth, contenttypes, products, sessions
# Running migrations:
#   Applying products.0001_initial... OK
```

🎉 **Your database table is now created!**

---

### Step 5: Interacting with the Model

#### Using Django Shell:

```bash
# Start Django's interactive Python shell
python manage.py shell
```

#### Creating Objects:

```python
# Import the model
from products.models import Product

# Method 1: Create and save separately
product = Product()
product.name = "Laptop"
product.description = "High-performance laptop"
product.price = 999.99
product.stock_quantity = 50
product.save()  # Saves to database

# Method 2: Create and save in one step
product2 = Product.objects.create(
    name="Mouse",
    description="Wireless mouse",
    price=29.99,
    stock_quantity=100
)

# Method 3: Create multiple objects
products = [
    Product(name="Keyboard", description="Mechanical keyboard", 
            price=79.99, stock_quantity=30),
    Product(name="Monitor", description="27-inch 4K monitor", 
            price=399.99, stock_quantity=20),
    Product(name="Webcam", description="HD webcam", 
            price=59.99, stock_quantity=45),
]
Product.objects.bulk_create(products)
```

#### Reading Objects:

```python
# Get all products
all_products = Product.objects.all()
print(all_products)
# <QuerySet [<Product: Laptop>, <Product: Mouse>, <Product: Keyboard>, ...]>

# Get a single product by ID
product = Product.objects.get(id=1)
print(product.name)  # Output: Laptop

# Get a single product by name
product = Product.objects.get(name="Mouse")
print(product.price)  # Output: 29.99

# Filter products
expensive_products = Product.objects.filter(price__gt=100)
in_stock = Product.objects.filter(stock_quantity__gt=0)
active_products = Product.objects.filter(is_active=True)
```

#### Updating Objects:

```python
# Method 1: Update single object
product = Product.objects.get(name="Laptop")
product.price = 899.99  # Discount!
product.save()

# Method 2: Update multiple objects
Product.objects.filter(stock_quantity=0).update(is_active=False)

# Method 3: Update and save in one line
Product.objects.filter(name="Mouse").update(price=24.99)
```

#### Deleting Objects:

```python
# Delete single object
product = Product.objects.get(name="Webcam")
product.delete()

# Delete multiple objects
Product.objects.filter(is_active=False).delete()

# Delete all objects (be careful!)
# Product.objects.all().delete()
```

---

### Step 6: Complete Example - Product Management

```python
from products.models import Product

# === CREATE ===
# Add new products
laptop = Product.objects.create(
    name="Gaming Laptop",
    description="High-end gaming laptop with RTX 4080",
    price=1999.99,
    stock_quantity=15
)

mouse = Product.objects.create(
    name="Gaming Mouse",
    description="RGB wireless gaming mouse",
    price=79.99,
    stock_quantity=50
)

# === READ ===
# Display all products
print("All Products:")
for product in Product.objects.all():
    print(f"- {product.name}: ${product.price} ({product.stock_quantity} in stock)")

# === UPDATE ===
# Apply discount to expensive products
expensive = Product.objects.filter(price__gte=1000)
for product in expensive:
    product.price = product.price * 0.9  # 10% discount
    product.save()
    print(f"Applied discount to {product.name}")

# === DELETE ===
# Remove out-of-stock products
out_of_stock = Product.objects.filter(stock_quantity=0)
count = out_of_stock.count()
out_of_stock.delete()
print(f"Deleted {count} out-of-stock products")

# === ADVANCED QUERIES ===
# Products between $50 and $500
mid_range = Product.objects.filter(price__gte=50, price__lte=500)

# Products with "gaming" in name (case-insensitive)
gaming_products = Product.objects.filter(name__icontains="gaming")

# Get product count
total_products = Product.objects.count()
print(f"Total products: {total_products}")

# Get the most expensive product
most_expensive = Product.objects.order_by('-price').first()
print(f"Most expensive: {most_expensive.name} - ${most_expensive.price}")

# Get products ordered by name
products_by_name = Product.objects.order_by('name')
```

---

## 🔍 Understanding the Database Table

After creating the Product model, Django creates this table structure:

```sql
-- Table: products_product
CREATE TABLE products_product (
    id INTEGER PRIMARY KEY AUTOINCREMENT,  -- Auto-generated
    name VARCHAR(200) NOT NULL,
    description TEXT NOT NULL,
    price DECIMAL(10, 2) NOT NULL,
    stock_quantity INTEGER NOT NULL,
    is_active BOOLEAN NOT NULL,
    created_at DATETIME NOT NULL,
    updated_at DATETIME NOT NULL
);
```

**Key Points:**
- Django automatically adds an `id` field (primary key)
- Field types are converted to appropriate SQL types
- Table name is `appname_modelname` (products_product)
- You can customize the table name in Meta class

---

## 💡 Best Practices

### ✅ DO:

1. **Use descriptive model names**: `Product`, `Order`, `Customer` (singular, not plural)
2. **Add `__str__` method**: Makes debugging easier
3. **Use appropriate field types**: Don't use CharField for numbers!
4. **Set default values**: Helps prevent errors
5. **Add docstrings**: Document what the model represents
6. **Use `blank=True` carefully**: Only when field can be empty
7. **Add validators**: Ensure data integrity

### ❌ DON'T:

1. **Don't use generic names**: Avoid `Data`, `Info`, `Item`
2. **Don't make everything optional**: Required fields should be required
3. **Don't skip migrations**: Always run makemigrations and migrate
4. **Don't use FloatField for money**: Use DecimalField instead
5. **Don't store files in database**: Use FileField/ImageField

---

## ✏️ Practice Exercise

### Exercise 2.1: Create a Book Model

**Task:** Create a Book model for a library management system.

**Requirements:**
```python
# books/models.py

class Book(models.Model):
    # Add these fields:
    # 1. title - up to 200 characters
    # 2. author - up to 100 characters
    # 3. isbn - exactly 13 characters (ISBN-13 format)
    # 4. publication_date - date field
    # 5. pages - positive integer
    # 6. price - decimal with 2 decimal places
    # 7. is_available - boolean, default True
    # 8. description - long text, can be blank
    # 9. created_at - auto timestamp
    # 10. updated_at - auto timestamp on save
    
    def __str__(self):
        # Return: "Title by Author"
        pass
    
    class Meta:
        # Order by title alphabetically
        # Set verbose names
        pass
```

**Steps:**
1. Create a 'books' app
2. Define the Book model with all fields
3. Run makemigrations and migrate
4. Use Django shell to create 5 books
5. Query books published after 2020
6. Update prices for books with more than 500 pages
7. Delete books that are not available

**Expected Output:**
```python
>>> Book.objects.count()
5
>>> Book.objects.filter(pages__gt=500).count()
2
>>> Book.objects.filter(publication_date__year__gte=2020)
<QuerySet [<Book: Python Crash Course by Eric Matthes>, ...]>
```

---

### Exercise 2.2: Product Inventory System

**Scenario:** You're building an inventory management system.

**Task:** Create these models:

```python
# 1. Category model
class Category(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField(blank=True)
    
# 2. Enhanced Product model
class Product(models.Model):
    # Add these additional fields to the Product model:
    # - sku (Stock Keeping Unit) - unique 10-character code
    # - category - relationship to Category (we'll learn this in detail later)
    # - cost_price - what you paid for it
    # - selling_price - what you sell it for
    # - minimum_stock_level - alert threshold
    
    @property
    def profit_margin(self):
        # Calculate profit percentage
        pass
    
    @property
    def needs_restock(self):
        # Return True if stock is below minimum level
        pass
```

**Tasks:**
1. Create 3 categories (Electronics, Books, Clothing)
2. Create 10 products across different categories
3. Find products that need restocking
4. Calculate total inventory value
5. Find products with >50% profit margin

---

## 🎓 Key Takeaways

1. ✅ Models are Python classes that represent database tables
2. ✅ Django ORM eliminates the need to write SQL
3. ✅ Each model inherits from `models.Model`
4. ✅ Use `makemigrations` and `migrate` to create tables
5. ✅ Use `objects.create()`, `filter()`, `get()` for CRUD operations
6. ✅ Always add `__str__` method for better representation
7. ✅ Use appropriate field types for different data

---

## 🔗 Additional Resources

- [Django Model Documentation](https://docs.djangoproject.com/en/4.2/topics/db/models/)
- [Django ORM Cookbook](https://books.agiliq.com/projects/django-orm-cookbook/)
- [Model Field Reference](https://docs.djangoproject.com/en/4.2/ref/models/fields/)

---

## 📚 Next Steps

Now that you understand models, let's explore all the available field types!

[← Back to Part 2](./README.md) | [Next: Field Types & Options →](./02-field-types.md)
