# Django ORM & QuerySets

## 📋 Table of Contents
- [WHY - Why Use Django ORM?](#why---why-use-django-orm)
- [WHEN - When to Use QuerySets?](#when---when-to-use-querysets)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use Django ORM?

Django's ORM (Object-Relational Mapping) lets you interact with your database using Python code instead of SQL. QuerySets are the API you use to query your database.

### 🎭 Real-Life Analogy: The Library Catalog System

Imagine a library:
- **Without ORM (Raw SQL)**: You have to write specific instructions in a technical language to find books: "SELECT * FROM books WHERE author='Smith' AND year>2020"
- **With ORM (Django QuerySets)**: You ask in natural Python: `Book.objects.filter(author='Smith', year__gt=2020)` - much more readable and Pythonic!

### Benefits of Django ORM:

- ✅ **No SQL Required**: Write Python instead of SQL
- ✅ **Database Agnostic**: Code works across different databases
- ✅ **SQL Injection Protection**: Automatic query parameterization
- ✅ **Lazy Evaluation**: Queries only execute when needed
- ✅ **Chainable**: Combine multiple filters elegantly
- ✅ **Caching**: Automatic query result caching
- ✅ **Readable**: More Pythonic than raw SQL

---

## 2️⃣ WHEN - When to Use QuerySets?

### ✅ Use QuerySets For:

- Retrieving data from database
- Filtering data by criteria
- Ordering and sorting results
- Aggregating data (count, sum, average)
- Creating, updating, deleting records
- Complex queries with relationships
- 95% of your database operations

### ⚠️ Use Raw SQL When:

- Very complex queries QuerySet can't handle
- Database-specific features needed
- Performance-critical operations
- Legacy database integration
- (But try QuerySets first!)

---

## 3️⃣ HOW - Implementation

### Setup: Sample Product Model

```python
# products/models.py
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock_quantity = models.IntegerField(default=0)
    is_active = models.BooleanField(default=True)
    category = models.CharField(max_length=50)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.name
```

```bash
# Create and apply migrations
python manage.py makemigrations
python manage.py migrate

# Start Django shell
python manage.py shell
```

---

## 📖 QuerySet Methods Reference

### 1. Creating Objects

#### Method 1: Create and Save Separately
```python
from products.models import Product

# Create instance
product = Product()
product.name = "Laptop"
product.price = 999.99
product.stock_quantity = 50
product.category = "Electronics"
product.save()  # Saves to database

print(product.id)  # Auto-generated ID
# Output: 1
```

#### Method 2: Create in One Step
```python
# create() saves automatically
product = Product.objects.create(
    name="Mouse",
    price=29.99,
    stock_quantity=100,
    category="Electronics"
)
print(product.id)
# Output: 2
```

#### Method 3: Bulk Create (More Efficient)
```python
# Create multiple objects at once
products = [
    Product(name="Keyboard", price=79.99, stock_quantity=30, category="Electronics"),
    Product(name="Monitor", price=299.99, stock_quantity=20, category="Electronics"),
    Product(name="Webcam", price=59.99, stock_quantity=45, category="Electronics"),
    Product(name="Python Book", price=39.99, stock_quantity=50, category="Books"),
    Product(name="Django Book", price=44.99, stock_quantity=30, category="Books"),
]

# Single database query for all objects
Product.objects.bulk_create(products)
```

#### Method 4: get_or_create (Avoid Duplicates)
```python
# Get existing or create new
product, created = Product.objects.get_or_create(
    name="Laptop",
    defaults={
        'price': 999.99,
        'stock_quantity': 50,
        'category': 'Electronics'
    }
)

if created:
    print(f"Created new product: {product.name}")
else:
    print(f"Product already exists: {product.name}")
```

---

### 2. Retrieving Objects

#### all() - Get All Objects
```python
# Get all products
all_products = Product.objects.all()
print(all_products)
# <QuerySet [<Product: Laptop>, <Product: Mouse>, ...]>

# Iterate through QuerySet
for product in all_products:
    print(f"{product.name}: ${product.price}")
```

#### get() - Get Single Object
```python
# Get by ID (raises DoesNotExist if not found)
product = Product.objects.get(id=1)
print(product.name)
# Output: Laptop

# Get by unique field
product = Product.objects.get(name="Laptop")

# ⚠️ Raises MultipleObjectsReturned if >1 result
# ⚠️ Raises DoesNotExist if not found

# Safe way to use get()
try:
    product = Product.objects.get(name="Laptop")
except Product.DoesNotExist:
    print("Product not found")
except Product.MultipleObjectsReturned:
    print("Multiple products found")
```

#### first() & last() - Get First/Last Object
```python
# Get first product
first_product = Product.objects.first()

# Get last product
last_product = Product.objects.last()

# Get first with ordering
newest_product = Product.objects.order_by('-created_at').first()

# Returns None if no objects (safe)
product = Product.objects.filter(price__gt=10000).first()
if product:
    print(product.name)
else:
    print("No expensive products found")
```

---

### 3. Filtering Objects

#### filter() - Get Multiple Objects Matching Criteria
```python
# Single condition
electronics = Product.objects.filter(category="Electronics")

# Multiple conditions (AND)
cheap_electronics = Product.objects.filter(
    category="Electronics",
    price__lt=100
)

# Chaining filters (same as above)
cheap_electronics = Product.objects.filter(category="Electronics").filter(price__lt=100)
```

#### exclude() - Get Objects NOT Matching Criteria
```python
# Exclude electronics
non_electronics = Product.objects.exclude(category="Electronics")

# Exclude expensive products
affordable = Product.objects.exclude(price__gt=500)

# Combine filter and exclude
affordable_electronics = Product.objects.filter(
    category="Electronics"
).exclude(price__gt=500)
```

---

### 4. Field Lookups (The Power of QuerySets!)

#### Exact Match
```python
# Exact match (case-sensitive)
product = Product.objects.get(name__exact="Laptop")

# Case-insensitive exact match
product = Product.objects.get(name__iexact="laptop")
```

#### Contains
```python
# Contains substring (case-sensitive)
products = Product.objects.filter(name__contains="Book")

# Case-insensitive contains
products = Product.objects.filter(name__icontains="book")
# Finds: "Python Book", "Django BOOK", "cookbook", etc.
```

#### Starts With / Ends With
```python
# Starts with
products = Product.objects.filter(name__startswith="Python")

# Case-insensitive starts with
products = Product.objects.filter(name__istartswith="python")

# Ends with
products = Product.objects.filter(name__endswith="Book")

# Case-insensitive ends with
products = Product.objects.filter(name__iendswith="book")
```

#### Numeric Comparisons
```python
# Greater than
expensive = Product.objects.filter(price__gt=100)

# Greater than or equal
expensive = Product.objects.filter(price__gte=100)

# Less than
cheap = Product.objects.filter(price__lt=50)

# Less than or equal
cheap = Product.objects.filter(price__lte=50)

# Range (inclusive)
mid_range = Product.objects.filter(price__range=(50, 500))
# Equivalent to: price >= 50 AND price <= 500
```

#### In / Not In
```python
# In list
categories = ["Electronics", "Books"]
products = Product.objects.filter(category__in=categories)

# Not in list
products = Product.objects.exclude(category__in=categories)

# In QuerySet
ids = [1, 2, 3, 4, 5]
products = Product.objects.filter(id__in=ids)
```

#### Date Lookups
```python
from datetime import date, timedelta
from django.utils import timezone

# Specific date
products = Product.objects.filter(created_at__date=date(2024, 1, 15))

# Year
products_2024 = Product.objects.filter(created_at__year=2024)

# Month
january_products = Product.objects.filter(created_at__month=1)

# Day
products = Product.objects.filter(created_at__day=15)

# Greater than date
recent = Product.objects.filter(
    created_at__gte=timezone.now() - timedelta(days=7)
)

# Date range
products = Product.objects.filter(
    created_at__date__range=(date(2024, 1, 1), date(2024, 12, 31))
)
```

#### Null / Empty Checks
```python
# Is null
products = Product.objects.filter(description__isnull=True)

# Is not null
products = Product.objects.filter(description__isnull=False)

# Empty string (for text fields)
products = Product.objects.filter(description__exact='')

# Not empty
products = Product.objects.exclude(description__exact='')
```

---

### 5. Ordering & Sorting

```python
# Order by price (ascending)
products = Product.objects.order_by('price')

# Order by price (descending)
products = Product.objects.order_by('-price')

# Multiple ordering
products = Product.objects.order_by('category', '-price')
# Orders by category first, then by price (high to low) within category

# Reverse ordering
products = Product.objects.order_by('price').reverse()

# Random ordering
products = Product.objects.order_by('?')

# Order by related field (we'll cover this more with relationships)
# products = Product.objects.order_by('category__name')
```

---

### 6. Limiting & Slicing

```python
# First 5 products
products = Product.objects.all()[:5]

# Products 5-10 (pagination)
products = Product.objects.all()[5:10]

# Every other product
products = Product.objects.all()[::2]

# ⚠️ Negative indexing not supported
# products = Product.objects.all()[-1]  # ERROR!
# Use .last() instead
product = Product.objects.last()

# Combine with filtering and ordering
top_5_expensive = Product.objects.filter(
    is_active=True
).order_by('-price')[:5]
```

---

### 7. Aggregation & Counting

```python
from django.db.models import Count, Sum, Avg, Max, Min

# Count objects
total_products = Product.objects.count()
print(f"Total products: {total_products}")

# Count with filter
active_count = Product.objects.filter(is_active=True).count()

# Check if any exist
has_products = Product.objects.exists()
if has_products:
    print("We have products!")

# Aggregate functions
from django.db.models import Avg, Sum, Max, Min, Count

stats = Product.objects.aggregate(
    average_price=Avg('price'),
    total_stock=Sum('stock_quantity'),
    max_price=Max('price'),
    min_price=Min('price'),
    product_count=Count('id')
)

print(stats)
# {
#     'average_price': Decimal('129.99'),
#     'total_stock': 225,
#     'max_price': Decimal('999.99'),
#     'min_price': Decimal('29.99'),
#     'product_count': 7
# }

# Access individual values
print(f"Average price: ${stats['average_price']}")
print(f"Most expensive: ${stats['max_price']}")
```

---

### 8. Updating Objects

#### Update Single Object
```python
# Get and update
product = Product.objects.get(id=1)
product.price = 899.99
product.save()

# Update specific fields only (more efficient)
product = Product.objects.get(id=1)
product.price = 899.99
product.save(update_fields=['price'])
```

#### Update Multiple Objects
```python
# Update all products
Product.objects.all().update(is_active=True)

# Update with filter
Product.objects.filter(category="Electronics").update(stock_quantity=100)

# Update multiple fields
Product.objects.filter(price__lt=50).update(
    is_active=True,
    stock_quantity=0
)

# Update returns count
updated_count = Product.objects.filter(category="Books").update(price=34.99)
print(f"Updated {updated_count} products")
```

#### F Expressions (Update Based on Current Value)
```python
from django.db.models import F

# Increase price by 10%
Product.objects.all().update(price=F('price') * 1.1)

# Increase stock quantity by 100
Product.objects.filter(category="Electronics").update(
    stock_quantity=F('stock_quantity') + 100
)

# Copy value from another field
Product.objects.update(old_price=F('price'))

# Compare fields
out_of_stock = Product.objects.filter(stock_quantity__lte=F('minimum_stock'))
```

---

### 9. Deleting Objects

```python
# Delete single object
product = Product.objects.get(id=1)
product.delete()

# Delete multiple objects
Product.objects.filter(is_active=False).delete()

# Delete with specific criteria
deleted_count = Product.objects.filter(
    stock_quantity=0,
    is_active=False
).delete()
print(f"Deleted {deleted_count} products")

# Delete all (⚠️ Be careful!)
# Product.objects.all().delete()
```

---

### 10. Complex Queries with Q Objects

```python
from django.db.models import Q

# OR condition
products = Product.objects.filter(
    Q(category="Electronics") | Q(category="Books")
)
# Finds products in Electronics OR Books

# AND condition (same as regular filter)
products = Product.objects.filter(
    Q(category="Electronics") & Q(price__lt=100)
)

# NOT condition
products = Product.objects.filter(
    ~Q(category="Electronics")
)
# Finds all products except Electronics

# Complex combinations
products = Product.objects.filter(
    (Q(category="Electronics") & Q(price__lt=100)) |
    (Q(category="Books") & Q(price__lt=50))
)
# Electronics under $100 OR Books under $50

# Dynamic filters
search_term = "Python"
products = Product.objects.filter(
    Q(name__icontains=search_term) |
    Q(description__icontains=search_term)
)
# Search in name OR description
```

---

## 🎯 Complete QuerySet Examples

### Example 1: E-commerce Product Search

```python
from django.db.models import Q, F

def search_products(search_query, min_price=None, max_price=None, category=None):
    """
    Advanced product search with multiple filters.
    """
    # Start with all active products
    products = Product.objects.filter(is_active=True)
    
    # Search in name and description
    if search_query:
        products = products.filter(
            Q(name__icontains=search_query) |
            Q(description__icontains=search_query)
        )
    
    # Price range filter
    if min_price:
        products = products.filter(price__gte=min_price)
    if max_price:
        products = products.filter(price__lte=max_price)
    
    # Category filter
    if category:
        products = products.filter(category=category)
    
    # Order by relevance (products in stock first, then by price)
    products = products.filter(stock_quantity__gt=0).order_by('price')
    
    return products

# Usage
results = search_products(
    search_query="laptop",
    min_price=500,
    max_price=2000,
    category="Electronics"
)

for product in results:
    print(f"{product.name} - ${product.price} ({product.stock_quantity} in stock)")
```

### Example 2: Inventory Management

```python
from django.db.models import Sum, Count, Avg, F

def inventory_report():
    """
    Generate comprehensive inventory report.
    """
    # Total inventory value
    total_value = Product.objects.aggregate(
        total=Sum(F('price') * F('stock_quantity'))
    )['total']
    
    # Products by category
    by_category = Product.objects.values('category').annotate(
        count=Count('id'),
        total_stock=Sum('stock_quantity'),
        avg_price=Avg('price')
    ).order_by('-count')
    
    # Out of stock products
    out_of_stock = Product.objects.filter(stock_quantity=0).count()
    
    # Low stock products (less than 10)
    low_stock = Product.objects.filter(
        stock_quantity__gt=0,
        stock_quantity__lt=10
    ).order_by('stock_quantity')
    
    print("=" * 50)
    print("INVENTORY REPORT")
    print("=" * 50)
    print(f"Total Inventory Value: ${total_value:,.2f}")
    print(f"Out of Stock Products: {out_of_stock}")
    print(f"\nProducts by Category:")
    for cat in by_category:
        print(f"  {cat['category']}: {cat['count']} products, "
              f"{cat['total_stock']} units, "
              f"avg ${cat['avg_price']:.2f}")
    
    print(f"\nLow Stock Alert:")
    for product in low_stock:
        print(f"  {product.name}: Only {product.stock_quantity} left!")
    
    return {
        'total_value': total_value,
        'by_category': by_category,
        'out_of_stock': out_of_stock,
        'low_stock': low_stock,
    }

# Usage
report = inventory_report()
```

### Example 3: Batch Operations

```python
def apply_seasonal_discount(category, discount_percent):
    """
    Apply discount to all products in a category.
    """
    products = Product.objects.filter(category=category)
    
    # Store original prices
    products.update(original_price=F('price'))
    
    # Apply discount
    updated = products.update(
        price=F('price') * (1 - discount_percent / 100)
    )
    
    print(f"Applied {discount_percent}% discount to {updated} products in {category}")
    return updated

# Usage
apply_seasonal_discount("Electronics", 15)  # 15% off electronics

def restock_products(category, quantity):
    """
    Add stock to all products in category.
    """
    updated = Product.objects.filter(category=category).update(
        stock_quantity=F('stock_quantity') + quantity
    )
    print(f"Added {quantity} units to {updated} products")
    return updated

# Usage
restock_products("Books", 50)  # Add 50 units to all books
```

---

## 🚀 QuerySet Performance Tips

### 1. Lazy Evaluation

```python
# QuerySet is created but NO database query yet
products = Product.objects.filter(category="Electronics")

# Query executes when you:
# - Iterate over it
for product in products:  # ← Query executes here
    print(product.name)

# - Slice it
first_five = products[:5]  # ← Query executes here

# - Convert to list
product_list = list(products)  # ← Query executes here

# - Call len() or count()
total = len(products)  # ← Query executes here
```

### 2. QuerySet Caching

```python
# First query
products = Product.objects.all()

# Query executes and results cached
for product in products:
    print(product.name)

# Uses cache (no new query!)
for product in products:
    print(product.price)

# ⚠️ This doesn't cache!
for product in Product.objects.all():  # Query executes
    print(product.name)
for product in Product.objects.all():  # Query executes AGAIN!
    print(product.price)
```

### 3. Select Only Needed Fields

```python
# Get only specific fields (more efficient)
products = Product.objects.values('name', 'price')
# Returns: [{'name': 'Laptop', 'price': 999.99}, ...]

# As list of tuples
products = Product.objects.values_list('name', 'price')
# Returns: [('Laptop', 999.99), ...]

# Flat list of single field
names = Product.objects.values_list('name', flat=True)
# Returns: ['Laptop', 'Mouse', 'Keyboard', ...]
```

---

## ✏️ Practice Exercise

### Exercise 2.5: Book Query Practice

**Setup:**
```python
# Create sample data
from books.models import Book
from datetime import date

books_data = [
    {"title": "Python Crash Course", "author": "Eric Matthes", "price": 39.99, 
     "pages": 544, "publication_date": date(2023, 1, 15), "rating": 4.8},
    {"title": "Django for Beginners", "author": "William Vincent", "price": 44.99,
     "pages": 385, "publication_date": date(2023, 5, 20), "rating": 4.6},
    {"title": "Fluent Python", "author": "Luciano Ramalho", "price": 64.99,
     "pages": 792, "publication_date": date(2022, 4, 10), "rating": 4.9},
    {"title": "Clean Code", "author": "Robert Martin", "price": 49.99,
     "pages": 464, "publication_date": date(2008, 8, 1), "rating": 4.7},
    {"title": "Design Patterns", "author": "Gang of Four", "price": 54.99,
     "pages": 416, "publication_date": date(1994, 10, 31), "rating": 4.5},
]

for data in books_data:
    Book.objects.create(**data)
```

**Tasks:**

1. **Basic Queries**
   ```python
   # Find all books by "Eric Matthes"
   # Find books with more than 500 pages
   # Find books priced under $50
   # Find books published after 2020
   ```

2. **Complex Filters**
   ```python
   # Find Python books (title contains "Python")
   # Find expensive books (price > $50) with high ratings (> 4.5)
   # Find books NOT by "Robert Martin"
   # Find books published in 2023
   ```

3. **Aggregations**
   ```python
   # Count total books
   # Calculate average price
   # Find most expensive book
   # Find shortest book (fewest pages)
   # Calculate total pages of all books
   ```

4. **Advanced Queries**
   ```python
   # Find top 3 highest rated books
   # Find books with "Python" OR "Django" in title
   # Find books under $50 published after 2020
   # Find books with above-average price
   ```

**Expected Results:**
```python
>>> # Books by Eric Matthes
>>> books = Book.objects.filter(author="Eric Matthes")
>>> books.count()
1

>>> # Expensive, highly rated books
>>> books = Book.objects.filter(price__gt=50, rating__gt=4.5)
>>> for book in books:
...     print(f"{book.title}: ${book.price} - {book.rating}★")
Fluent Python: $64.99 - 4.9★
Design Patterns: $54.99 - 4.5★

>>> # Statistics
>>> from django.db.models import Avg, Max, Min, Sum
>>> stats = Book.objects.aggregate(
...     avg_price=Avg('price'),
...     max_pages=Max('pages'),
...     total_books=Count('id')
... )
>>> print(stats)
{'avg_price': Decimal('50.99'), 'max_pages': 792, 'total_books': 5}
```

---

### Exercise 2.6: Product Inventory Queries

**Tasks:**
1. Create 20 products across 4 categories
2. Find all electronics under $100
3. Find products out of stock
4. Calculate total inventory value per category
5. Find top 5 most expensive products
6. Apply 20% discount to all books
7. Increase stock by 50 for all products under $50
8. Find products added in the last 7 days
9. Search for products with "gaming" in name or description
10. Generate inventory report showing:
    - Total products
    - Products by category
    - Average price per category
    - Out of stock items
    - Total inventory value

---

## 🎓 Key Takeaways

1. ✅ Use `.all()` for all objects, `.filter()` for specific criteria
2. ✅ Use `.get()` for single objects, handle exceptions
3. ✅ Field lookups: `__gt`, `__lt`, `__contains`, `__icontains`, etc.
4. ✅ Chain methods: `.filter().exclude().order_by()`
5. ✅ Use Q objects for complex OR/NOT queries
6. ✅ Use F expressions to reference field values
7. ✅ Aggregate functions: Count, Sum, Avg, Max, Min
8. ✅ QuerySets are lazy - only execute when needed
9. ✅ Slice QuerySets for pagination: `[:10]`
10. ✅ Use `.exists()` to check if any objects match

---

## 🔗 Additional Resources

- [QuerySet API Reference](https://docs.djangoproject.com/en/4.2/ref/models/querysets/)
- [Making Queries](https://docs.djangoproject.com/en/4.2/topics/db/queries/)
- [Field Lookups Reference](https://docs.djangoproject.com/en/4.2/ref/models/querysets/#field-lookups)

---

[← Previous: Migrations](./03-migrations.md) | [Next: Admin Interface →](./05-admin-interface.md)
