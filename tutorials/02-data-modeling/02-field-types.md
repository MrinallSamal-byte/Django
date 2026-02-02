# Field Types & Options

## 📋 Table of Contents
- [WHY - Why Different Field Types?](#why---why-different-field-types)
- [WHEN - When to Use Each Field Type?](#when---when-to-use-each-field-type)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Different Field Types?

Different types of data require different storage methods and validation rules. Django provides specialized field types to handle various data correctly and efficiently.

### 🎭 Real-Life Analogy: The Filing Cabinet

Imagine organizing a filing cabinet:
- **Text files** go in regular folders (CharField, TextField)
- **Numbers** go in numerical folders with calculators (IntegerField, DecimalField)
- **Dates** go in a calendar system (DateField, DateTimeField)
- **True/False decisions** go in a yes/no box (BooleanField)
- **Photos** go in special photo albums (ImageField)

Using the wrong storage method causes problems! You wouldn't store a photo in a text folder or a date in a number folder.

### Benefits of Proper Field Types:

- ✅ **Data Validation**: Ensures data is in the correct format
- ✅ **Database Efficiency**: Optimized storage and indexing
- ✅ **Type Safety**: Prevents type errors at the database level
- ✅ **Form Generation**: Automatic form field generation
- ✅ **Better Queries**: Type-specific query operations
- ✅ **Admin Interface**: Appropriate widgets in admin panel

---

## 2️⃣ WHEN - When to Use Each Field Type?

### 📝 Text Fields

| Field Type | When to Use | Max Size | Example |
|-----------|-------------|----------|---------|
| **CharField** | Short text (names, titles, codes) | Required max_length | Product name, email, phone |
| **TextField** | Long text (descriptions, content) | Unlimited | Blog post, product description |
| **EmailField** | Email addresses | 254 chars | user@example.com |
| **URLField** | Website URLs | 200 chars | https://example.com |
| **SlugField** | URL-friendly strings | 50 chars | my-blog-post |

### 🔢 Numeric Fields

| Field Type | When to Use | Range | Example |
|-----------|-------------|-------|---------|
| **IntegerField** | Whole numbers | -2147483648 to 2147483647 | Age, quantity, count |
| **PositiveIntegerField** | Positive whole numbers | 0 to 2147483647 | Stock quantity, likes |
| **SmallIntegerField** | Small whole numbers | -32768 to 32767 | Rating (1-5) |
| **BigIntegerField** | Very large numbers | ±9 quintillion | Population, large IDs |
| **DecimalField** | Precise decimal numbers | Defined by max_digits | Prices, percentages |
| **FloatField** | Approximate decimals | Variable precision | Scientific calculations |

### 📅 Date & Time Fields

| Field Type | When to Use | Format | Example |
|-----------|-------------|--------|---------|
| **DateField** | Date only | YYYY-MM-DD | Birth date, publication date |
| **DateTimeField** | Date and time | YYYY-MM-DD HH:MM:SS | Created at, updated at |
| **TimeField** | Time only | HH:MM:SS | Opening hours, duration |
| **DurationField** | Time periods | timedelta | Video length, session duration |

### ✅ Boolean & Choice Fields

| Field Type | When to Use | Values | Example |
|-----------|-------------|--------|---------|
| **BooleanField** | True/False values | True, False | Is active, is published |
| **NullBooleanField** | True/False/Unknown | True, False, None | User preference (deprecated in Django 4+) |
| **CharField with choices** | Limited options | Predefined list | Status, category, priority |

### 📁 File & Media Fields

| Field Type | When to Use | Storage | Example |
|-----------|-------------|---------|---------|
| **FileField** | Any file upload | File system | PDF, document |
| **ImageField** | Images only | File system | Product photo, avatar |

---

## 3️⃣ HOW - Implementation

### Text Fields in Detail

```python
from django.db import models

class Product(models.Model):
    # CharField - Required max_length
    name = models.CharField(
        max_length=200,
        help_text="Product name"
    )
    
    # CharField with unique constraint
    sku = models.CharField(
        max_length=50,
        unique=True,  # Must be unique across all products
        db_index=True  # Create database index for faster queries
    )
    
    # TextField - Long text, no max_length needed
    description = models.TextField(
        blank=True,  # Can be empty in forms
        null=True,   # Can be NULL in database
        help_text="Detailed product description"
    )
    
    # EmailField - Validates email format
    contact_email = models.EmailField(
        max_length=254,
        blank=True,
        help_text="Contact email for product inquiries"
    )
    
    # URLField - Validates URL format
    product_url = models.URLField(
        max_length=200,
        blank=True,
        help_text="External product page URL"
    )
    
    # SlugField - URL-friendly string
    slug = models.SlugField(
        max_length=200,
        unique=True,
        help_text="URL slug for product page"
    )
    # Example: "gaming-laptop-rtx-4080" instead of "Gaming Laptop RTX 4080"
    
    def __str__(self):
        return self.name
```

**Using SlugField:**
```python
from django.utils.text import slugify

product = Product.objects.create(
    name="Gaming Laptop RTX 4080",
    slug=slugify("Gaming Laptop RTX 4080")  # Creates: "gaming-laptop-rtx-4080"
)
```

---

### Numeric Fields in Detail

```python
class Product(models.Model):
    # IntegerField - Standard integers
    quantity = models.IntegerField(
        default=0,
        help_text="Stock quantity"
    )
    
    # PositiveIntegerField - Only positive numbers
    views_count = models.PositiveIntegerField(
        default=0,
        help_text="Number of times product was viewed"
    )
    
    # SmallIntegerField - Small numbers (-32768 to 32767)
    rating = models.SmallIntegerField(
        default=0,
        choices=[(i, str(i)) for i in range(1, 6)],  # 1-5 rating
        help_text="Product rating (1-5 stars)"
    )
    
    # DecimalField - Precise decimal numbers (ALWAYS use for money!)
    price = models.DecimalField(
        max_digits=10,      # Total number of digits
        decimal_places=2,   # Digits after decimal point
        help_text="Product price"
    )
    # Example: 12345678.90 (10 total digits, 2 after decimal)
    
    # FloatField - Approximate decimals (NOT for money!)
    weight = models.FloatField(
        help_text="Product weight in kilograms"
    )
    
    # BigIntegerField - Very large numbers
    total_sales_cents = models.BigIntegerField(
        default=0,
        help_text="Total sales amount in cents"
    )
```

**Why DecimalField for Money:**
```python
# ❌ WRONG - FloatField has rounding errors
price = 0.1 + 0.2  # Result: 0.30000000000000004

# ✅ CORRECT - DecimalField is precise
from decimal import Decimal
price = Decimal('0.1') + Decimal('0.2')  # Result: 0.3
```

---

### Date & Time Fields in Detail

```python
from django.utils import timezone

class Product(models.Model):
    # DateField - Date only
    manufacture_date = models.DateField(
        help_text="Date of manufacture"
    )
    
    # DateField with auto_now_add - Set once on creation
    created_at = models.DateTimeField(
        auto_now_add=True,
        help_text="When product was added to system"
    )
    
    # DateField with auto_now - Update on every save
    updated_at = models.DateTimeField(
        auto_now=True,
        help_text="Last update timestamp"
    )
    
    # DateTimeField with default
    published_at = models.DateTimeField(
        default=timezone.now,  # Use timezone.now, not timezone.now()
        help_text="When product was published"
    )
    
    # TimeField - Time only
    delivery_time = models.TimeField(
        null=True,
        blank=True,
        help_text="Expected delivery time"
    )
    
    # DurationField - Time periods
    warranty_period = models.DurationField(
        null=True,
        blank=True,
        help_text="Warranty duration"
    )
```

**Working with Date/Time Fields:**
```python
from datetime import date, time, timedelta
from django.utils import timezone

# Create product with specific dates
product = Product.objects.create(
    name="Laptop",
    manufacture_date=date(2024, 1, 15),
    delivery_time=time(14, 30),  # 2:30 PM
    warranty_period=timedelta(days=365)  # 1 year
)

# Query by date
recent_products = Product.objects.filter(
    created_at__gte=timezone.now() - timedelta(days=7)
)

# Query by year
products_2024 = Product.objects.filter(manufacture_date__year=2024)
```

---

### Boolean Fields in Detail

```python
class Product(models.Model):
    # BooleanField - Required True/False
    is_active = models.BooleanField(
        default=True,
        help_text="Is product active and visible?"
    )
    
    # BooleanField - Another example
    is_featured = models.BooleanField(
        default=False,
        db_index=True,  # Index for faster featured product queries
        help_text="Show on featured products page"
    )
    
    # BooleanField with custom name
    in_stock = models.BooleanField(
        default=True,
        verbose_name="In Stock",
        help_text="Is product currently in stock?"
    )
```

**Using Boolean Fields:**
```python
# Create product
product = Product.objects.create(name="Mouse", is_active=True)

# Query active products
active_products = Product.objects.filter(is_active=True)

# Toggle boolean
product.is_featured = not product.is_featured
product.save()

# Update multiple
Product.objects.filter(quantity=0).update(in_stock=False)
```

---

### Choice Fields in Detail

```python
class Product(models.Model):
    # Define choices as tuples: (value_stored_in_db, human_readable_name)
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('active', 'Active'),
        ('archived', 'Archived'),
        ('discontinued', 'Discontinued'),
    ]
    
    status = models.CharField(
        max_length=20,
        choices=STATUS_CHOICES,
        default='draft',
        help_text="Product status"
    )
    
    # Integer choices
    PRIORITY_CHOICES = [
        (1, 'Low'),
        (2, 'Medium'),
        (3, 'High'),
        (4, 'Urgent'),
    ]
    
    priority = models.IntegerField(
        choices=PRIORITY_CHOICES,
        default=2,
        help_text="Product priority level"
    )
    
    # Using TextChoices (Django 3.0+) - More Pythonic
    class Category(models.TextChoices):
        ELECTRONICS = 'ELEC', 'Electronics'
        BOOKS = 'BOOK', 'Books'
        CLOTHING = 'CLTH', 'Clothing'
        FOOD = 'FOOD', 'Food & Beverages'
        TOYS = 'TOYS', 'Toys & Games'
    
    category = models.CharField(
        max_length=4,
        choices=Category.choices,
        default=Category.ELECTRONICS,
        help_text="Product category"
    )
    
    # Using IntegerChoices
    class Size(models.IntegerChoices):
        SMALL = 1, 'Small (S)'
        MEDIUM = 2, 'Medium (M)'
        LARGE = 3, 'Large (L)'
        XLARGE = 4, 'Extra Large (XL)'
    
    size = models.IntegerField(
        choices=Size.choices,
        null=True,
        blank=True,
        help_text="Product size (for applicable products)"
    )
```

**Working with Choice Fields:**
```python
# Create with choices
product = Product.objects.create(
    name="Laptop",
    status='active',
    priority=3,
    category=Product.Category.ELECTRONICS,
    size=Product.Size.LARGE
)

# Access choice display value
print(product.status)  # Output: 'active'
print(product.get_status_display())  # Output: 'Active'

print(product.category)  # Output: 'ELEC'
print(product.get_category_display())  # Output: 'Electronics'

# Query by choice
electronics = Product.objects.filter(category=Product.Category.ELECTRONICS)
high_priority = Product.objects.filter(priority__gte=3)
```

---

### File & Image Fields

```python
class Product(models.Model):
    # ImageField - Requires Pillow package
    image = models.ImageField(
        upload_to='products/images/%Y/%m/%d/',  # Organize by date
        null=True,
        blank=True,
        help_text="Product image"
    )
    
    # FileField - Any file type
    manual = models.FileField(
        upload_to='products/manuals/',
        null=True,
        blank=True,
        help_text="Product manual PDF"
    )
    
    # Multiple images (we'll use a related model for this)
    # This is just an example - normally you'd use a separate model
```

**Setup for File/Image Fields:**

```python
# settings.py
MEDIA_URL = '/media/'
MEDIA_ROOT = BASE_DIR / 'media'

# urls.py (for development)
from django.conf import settings
from django.conf.urls.static import static

urlpatterns = [
    # ... your urls
]

if settings.DEBUG:
    urlpatterns += static(settings.MEDIA_URL, document_root=settings.MEDIA_ROOT)
```

**Install Pillow for ImageField:**
```bash
pip install Pillow
```

---

### Common Field Options

All fields accept these common options:

```python
class Product(models.Model):
    name = models.CharField(
        max_length=200,
        
        # Value Options
        default='Unnamed Product',  # Default value if not provided
        null=False,                 # Can be NULL in database (default: False)
        blank=False,                # Can be empty in forms (default: False)
        
        # Validation Options
        unique=False,               # Must be unique (default: False)
        choices=None,               # Limit to specific choices
        
        # Database Options
        db_index=False,             # Create database index (default: False)
        db_column=None,             # Custom database column name
        
        # Display Options
        verbose_name='Product Name',  # Human-readable name
        help_text='Enter product name',  # Help text for forms
        
        # Other Options
        editable=True,              # Show in forms (default: True)
        primary_key=False,          # Use as primary key (default: False)
    )
```

**Understanding `null` vs `blank`:**

```python
# null=False, blank=False (DEFAULT)
name = models.CharField(max_length=100)
# Database: NOT NULL
# Forms: Required field

# null=True, blank=True
description = models.TextField(null=True, blank=True)
# Database: Can be NULL
# Forms: Optional field

# null=False, blank=True
bio = models.TextField(blank=True, default='')
# Database: NOT NULL (empty string stored)
# Forms: Optional field

# null=True, blank=False (RARE - usually not useful)
weird_field = models.CharField(max_length=100, null=True, blank=False)
# Database: Can be NULL
# Forms: Required field (but can save NULL programmatically)
```

**Best Practice:**
- For text fields (CharField, TextField): Use `blank=True` with `default=''`
- For other fields: Use `null=True, blank=True` together

---

## 🎯 Complete Product Model Example

```python
from django.db import models
from django.utils.text import slugify
from django.utils import timezone

class Product(models.Model):
    """
    Complete product model with various field types.
    """
    
    # === Text Fields ===
    name = models.CharField(
        max_length=200,
        help_text="Product name"
    )
    
    slug = models.SlugField(
        max_length=200,
        unique=True,
        help_text="URL-friendly product identifier"
    )
    
    sku = models.CharField(
        max_length=50,
        unique=True,
        db_index=True,
        help_text="Stock Keeping Unit"
    )
    
    description = models.TextField(
        blank=True,
        help_text="Detailed product description"
    )
    
    # === Numeric Fields ===
    price = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        help_text="Selling price"
    )
    
    cost = models.DecimalField(
        max_digits=10,
        decimal_places=2,
        help_text="Cost price"
    )
    
    quantity = models.PositiveIntegerField(
        default=0,
        help_text="Stock quantity"
    )
    
    weight = models.FloatField(
        null=True,
        blank=True,
        help_text="Weight in kilograms"
    )
    
    # === Choice Fields ===
    class Status(models.TextChoices):
        DRAFT = 'draft', 'Draft'
        ACTIVE = 'active', 'Active'
        ARCHIVED = 'archived', 'Archived'
    
    status = models.CharField(
        max_length=20,
        choices=Status.choices,
        default=Status.DRAFT
    )
    
    class Category(models.TextChoices):
        ELECTRONICS = 'electronics', 'Electronics'
        BOOKS = 'books', 'Books'
        CLOTHING = 'clothing', 'Clothing'
        FOOD = 'food', 'Food'
    
    category = models.CharField(
        max_length=20,
        choices=Category.choices,
        default=Category.ELECTRONICS
    )
    
    # === Boolean Fields ===
    is_featured = models.BooleanField(
        default=False,
        db_index=True
    )
    
    is_active = models.BooleanField(
        default=True
    )
    
    # === Date/Time Fields ===
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    published_at = models.DateTimeField(null=True, blank=True)
    
    # === File Fields ===
    image = models.ImageField(
        upload_to='products/%Y/%m/',
        null=True,
        blank=True
    )
    
    # === Calculated Properties ===
    @property
    def profit_margin(self):
        """Calculate profit margin percentage."""
        if self.cost > 0:
            return ((self.price - self.cost) / self.cost) * 100
        return 0
    
    @property
    def in_stock(self):
        """Check if product is in stock."""
        return self.quantity > 0
    
    # === Model Methods ===
    def save(self, *args, **kwargs):
        """Auto-generate slug if not provided."""
        if not self.slug:
            self.slug = slugify(self.name)
        super().save(*args, **kwargs)
    
    def __str__(self):
        return f"{self.name} ({self.sku})"
    
    class Meta:
        ordering = ['-created_at']
        verbose_name = 'Product'
        verbose_name_plural = 'Products'
        indexes = [
            models.Index(fields=['category', 'status']),
            models.Index(fields=['price']),
        ]
```

---

## ✏️ Practice Exercise

### Exercise 2.1: Create a Book Model with Various Field Types

**Task:** Create a comprehensive Book model using different field types.

```python
# books/models.py
from django.db import models

class Book(models.Model):
    """
    Complete the Book model with appropriate field types.
    """
    
    # Text Fields
    title = # CharField, max 200, required
    author = # CharField, max 100, required
    isbn = # CharField, max 13, unique, required
    publisher = # CharField, max 100, optional
    description = # TextField, optional
    
    # Numeric Fields
    pages = # PositiveIntegerField, required
    price = # DecimalField, max 8 digits, 2 decimals
    stock_quantity = # PositiveIntegerField, default 0
    edition = # PositiveSmallIntegerField, default 1
    rating = # DecimalField for ratings (1.0 to 5.0), 1 decimal
    
    # Date Fields
    publication_date = # DateField
    created_at = # DateTimeField, auto on create
    updated_at = # DateTimeField, auto on update
    
    # Choice Fields
    class Format(models.TextChoices):
        HARDCOVER = 'hardcover', 'Hardcover'
        PAPERBACK = 'paperback', 'Paperback'
        EBOOK = 'ebook', 'E-Book'
        AUDIOBOOK = 'audiobook', 'Audiobook'
    
    format = # CharField with Format choices
    
    class Language(models.TextChoices):
        ENGLISH = 'en', 'English'
        SPANISH = 'es', 'Spanish'
        FRENCH = 'fr', 'French'
        GERMAN = 'de', 'German'
        CHINESE = 'zh', 'Chinese'
    
    language = # CharField with Language choices, default English
    
    # Boolean Fields
    is_bestseller = # BooleanField, default False
    is_available = # BooleanField, default True
    
    # File Fields
    cover_image = # ImageField, upload to 'books/covers/', optional
    
    # Methods
    def __str__(self):
        return f"{self.title} by {self.author}"
    
    class Meta:
        ordering = ['-created_at']
        verbose_name = 'Book'
        verbose_name_plural = 'Books'
```

**Tasks:**
1. Complete all field definitions with appropriate types
2. Run makemigrations and migrate
3. Create 10 books with various field values
4. Query books by different criteria
5. Test choice field display methods

**Expected Results:**
```python
>>> Book.objects.count()
10
>>> book = Book.objects.first()
>>> book.get_format_display()
'Paperback'
>>> Book.objects.filter(is_bestseller=True).count()
3
>>> Book.objects.filter(price__lte=20).count()
5
```

---

### Exercise 2.2: E-commerce Product Catalog

**Scenario:** Create a complete product catalog with all field types.

```python
class Product(models.Model):
    # Implement all these requirements:
    # 1. Basic info: name, slug, sku, description
    # 2. Pricing: price, cost, discount_percentage
    # 3. Inventory: quantity, minimum_stock_level, maximum_stock_level
    # 4. Categories: Use choices for category and subcategory
    # 5. Status: draft, active, out_of_stock, discontinued
    # 6. Ratings: average_rating (1-5 stars), total_reviews
    # 7. Dimensions: weight, length, width, height
    # 8. Media: main_image, thumbnail
    # 9. Timestamps: created, updated, published
    # 10. Flags: is_featured, is_on_sale, is_new_arrival
    
    # Add properties:
    @property
    def discounted_price(self):
        # Calculate price after discount
        pass
    
    @property
    def profit_amount(self):
        # Calculate profit per unit
        pass
    
    @property
    def needs_restock(self):
        # True if quantity < minimum_stock_level
        pass
```

**Test Cases:**
```python
# 1. Create products with various attributes
# 2. Find products on sale
# 3. Find products needing restock
# 4. Calculate total inventory value
# 5. Find products by category
# 6. Find highly rated products (rating > 4.0)
# 7. Apply bulk discount to all electronics
# 8. List new arrivals from last 30 days
```

---

## 🎓 Key Takeaways

1. ✅ Use CharField for short text, TextField for long text
2. ✅ Always use DecimalField for monetary values, never FloatField
3. ✅ Use auto_now_add for created timestamps, auto_now for updated
4. ✅ BooleanField for True/False, choices for limited options
5. ✅ Use null=True/blank=True carefully - understand the difference
6. ✅ ImageField requires Pillow package
7. ✅ Add db_index=True for fields you'll query frequently
8. ✅ Use TextChoices/IntegerChoices for better choice management

---

## 🔗 Additional Resources

- [Django Field Types Reference](https://docs.djangoproject.com/en/4.2/ref/models/fields/)
- [Field Options Documentation](https://docs.djangoproject.com/en/4.2/ref/models/fields/#field-options)
- [Model Field Validation](https://docs.djangoproject.com/en/4.2/ref/validators/)

---

[← Previous: Models Introduction](./01-models-intro.md) | [Next: Migrations →](./03-migrations.md)
