# The Django Admin Interface

## 📋 Table of Contents
- [WHY - Why Use Django Admin?](#why---why-use-django-admin)
- [WHEN - When to Use Admin Interface?](#when---when-to-use-admin-interface)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use Django Admin?

The Django Admin is an automatically generated, production-ready interface for managing your site's data. It reads metadata from your models to provide a powerful and customizable admin panel.

### 🎭 Real-Life Analogy: The Control Room

Imagine managing a warehouse:
- **Without Admin**: You manually write forms, views, and templates to add/edit/delete products. Hours of repetitive work!
- **With Admin**: Django automatically creates a professional control panel with authentication, permissions, search, filters, and CRUD operations. Zero code required!

### Benefits of Django Admin:

- ✅ **Zero Setup**: Works out of the box
- ✅ **Automatic CRUD**: Create, Read, Update, Delete operations
- ✅ **User Authentication**: Built-in login system
- ✅ **Permissions**: Role-based access control
- ✅ **Customizable**: Highly flexible and extensible
- ✅ **Professional UI**: Clean, responsive interface
- ✅ **Search & Filters**: Advanced data filtering
- ✅ **Bulk Actions**: Modify multiple records at once
- ✅ **Production Ready**: Used by thousands of sites

---

## 2️⃣ WHEN - When to Use Admin Interface?

### ✅ Perfect For:

- **Content Management**: Blog posts, pages, articles
- **Internal Tools**: Managing data for staff
- **Quick Prototyping**: Rapid application development
- **Data Entry**: Bulk data input and editing
- **Testing**: Quickly populate database with test data
- **Small to Medium Projects**: Complete admin solution

### ⚠️ Not Ideal For:

- **Public-Facing Interface**: End users shouldn't access admin
- **Complex Workflows**: Multi-step business processes
- **Highly Custom UI**: When you need very specific design
- **Mobile-First Apps**: Admin is desktop-optimized

### Common Use Cases:

1. **Blog/CMS**: Managing posts, pages, comments
2. **E-commerce**: Managing products, orders, inventory
3. **User Management**: Admin managing regular users
4. **Data Import**: Quickly adding reference data
5. **Reports**: Viewing and filtering data

---

## 3️⃣ HOW - Implementation

### Step 1: Create a Superuser

```bash
# Create admin account
python manage.py createsuperuser
```

**Prompts:**
```
Username: admin
Email address: admin@example.com
Password: ********
Password (again): ********
Superuser created successfully.
```

**Start Development Server:**
```bash
python manage.py runserver
```

**Access Admin:**
```
http://127.0.0.1:8000/admin/
```

---

### Step 2: Basic Model Registration

```python
# products/models.py
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    description = models.TextField(blank=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    stock_quantity = models.IntegerField(default=0)
    is_active = models.BooleanField(default=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.name
```

```python
# products/admin.py
from django.contrib import admin
from .models import Product

# Basic registration
admin.site.register(Product)
```

**That's it!** Visit `/admin/` and you'll see the Product model with full CRUD functionality.

---

### Step 3: Customizing the Admin Display

#### List Display - Choose Which Columns to Show

```python
# products/admin.py
from django.contrib import admin
from .models import Product

class ProductAdmin(admin.ModelAdmin):
    # Display these fields in the list view
    list_display = ['name', 'price', 'stock_quantity', 'is_active', 'created_at']
    
    # Make these fields clickable links
    list_display_links = ['name']
    
    # Add edit fields directly in list view
    list_editable = ['price', 'stock_quantity', 'is_active']
    
    # Add filters sidebar
    list_filter = ['is_active', 'created_at']
    
    # Add search functionality
    search_fields = ['name', 'description']
    
    # Set items per page
    list_per_page = 20
    
    # Default ordering
    ordering = ['-created_at']

# Register with custom admin class
admin.site.register(Product, ProductAdmin)
```

**Result:** Professional admin interface with search, filters, and editable fields!

---

### Step 4: Organizing Form Fields

```python
from django.contrib import admin
from .models import Product

class ProductAdmin(admin.ModelAdmin):
    list_display = ['name', 'price', 'stock_quantity', 'is_active']
    
    # Organize fields into sections
    fieldsets = (
        ('Basic Information', {
            'fields': ('name', 'description')
        }),
        ('Pricing & Inventory', {
            'fields': ('price', 'stock_quantity')
        }),
        ('Status', {
            'fields': ('is_active',),
            'classes': ('collapse',),  # Collapsible section
        }),
        ('Timestamps', {
            'fields': ('created_at', 'updated_at'),
            'classes': ('collapse',),
        }),
    )
    
    # Make timestamps read-only
    readonly_fields = ['created_at', 'updated_at']
    
    # Pre-populate slug from name (if you have slug field)
    # prepopulated_fields = {'slug': ('name',)}

admin.site.register(Product, ProductAdmin)
```

---

### Step 5: Advanced Customizations

#### Custom Display Methods

```python
from django.contrib import admin
from django.utils.html import format_html
from .models import Product

class ProductAdmin(admin.ModelAdmin):
    list_display = [
        'name', 
        'formatted_price',  # Custom method
        'stock_status',     # Custom method
        'is_active',
        'colored_status'    # Custom method with HTML
    ]
    
    # Custom method: Format price
    def formatted_price(self, obj):
        return f"${obj.price:.2f}"
    formatted_price.short_description = 'Price'  # Column header
    formatted_price.admin_order_field = 'price'  # Enable sorting
    
    # Custom method: Stock status
    def stock_status(self, obj):
        if obj.stock_quantity == 0:
            return 'Out of Stock'
        elif obj.stock_quantity < 10:
            return f'Low Stock ({obj.stock_quantity})'
        else:
            return f'In Stock ({obj.stock_quantity})'
    stock_status.short_description = 'Stock Status'
    
    # Custom method: Colored status with HTML
    def colored_status(self, obj):
        if obj.is_active:
            color = 'green'
            text = '✓ Active'
        else:
            color = 'red'
            text = '✗ Inactive'
        return format_html(
            '<span style="color: {};">{}</span>',
            color,
            text
        )
    colored_status.short_description = 'Status'
    colored_status.admin_order_field = 'is_active'

admin.site.register(Product, ProductAdmin)
```

---

### Step 6: Adding Filters

```python
from django.contrib import admin
from django.utils import timezone
from datetime import timedelta
from .models import Product

# Custom filter
class StockFilter(admin.SimpleListFilter):
    title = 'stock status'
    parameter_name = 'stock'
    
    def lookups(self, request, model_admin):
        return (
            ('in_stock', 'In Stock'),
            ('low_stock', 'Low Stock'),
            ('out_of_stock', 'Out of Stock'),
        )
    
    def queryset(self, request, queryset):
        if self.value() == 'in_stock':
            return queryset.filter(stock_quantity__gte=10)
        if self.value() == 'low_stock':
            return queryset.filter(stock_quantity__gt=0, stock_quantity__lt=10)
        if self.value() == 'out_of_stock':
            return queryset.filter(stock_quantity=0)

class ProductAdmin(admin.ModelAdmin):
    list_display = ['name', 'price', 'stock_quantity', 'is_active']
    
    # Add filters
    list_filter = [
        'is_active',
        'created_at',
        StockFilter,  # Custom filter
    ]
    
    # Date hierarchy navigation
    date_hierarchy = 'created_at'
    
    search_fields = ['name', 'description']

admin.site.register(Product, ProductAdmin)
```

---

### Step 7: Bulk Actions

```python
from django.contrib import admin
from .models import Product

class ProductAdmin(admin.ModelAdmin):
    list_display = ['name', 'price', 'stock_quantity', 'is_active']
    
    # Enable bulk actions
    actions = ['activate_products', 'deactivate_products', 'apply_discount']
    
    # Custom bulk action: Activate products
    def activate_products(self, request, queryset):
        updated = queryset.update(is_active=True)
        self.message_user(request, f'{updated} products activated.')
    activate_products.short_description = 'Activate selected products'
    
    # Custom bulk action: Deactivate products
    def deactivate_products(self, request, queryset):
        updated = queryset.update(is_active=False)
        self.message_user(request, f'{updated} products deactivated.')
    deactivate_products.short_description = 'Deactivate selected products'
    
    # Custom bulk action: Apply discount
    def apply_discount(self, request, queryset):
        from django.db.models import F
        updated = queryset.update(price=F('price') * 0.9)  # 10% off
        self.message_user(request, f'Applied 10% discount to {updated} products.')
    apply_discount.short_description = 'Apply 10% discount'

admin.site.register(Product, ProductAdmin)
```

**Usage:** Select products, choose action from dropdown, click "Go"

---

### Step 8: Inline Models (Related Objects)

```python
# models.py
from django.db import models

class Category(models.Model):
    name = models.CharField(max_length=100)
    description = models.TextField(blank=True)
    
    def __str__(self):
        return self.name
    
    class Meta:
        verbose_name_plural = 'Categories'

class Product(models.Model):
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    
    def __str__(self):
        return self.name

class ProductImage(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to='products/')
    caption = models.CharField(max_length=200, blank=True)
    
    def __str__(self):
        return f"Image for {self.product.name}"
```

```python
# admin.py
from django.contrib import admin
from .models import Category, Product, ProductImage

# Inline for product images
class ProductImageInline(admin.TabularInline):
    model = ProductImage
    extra = 1  # Number of empty forms to display
    fields = ['image', 'caption']

# Inline for products in category
class ProductInline(admin.TabularInline):
    model = Product
    extra = 0
    fields = ['name', 'price', 'is_active']
    show_change_link = True  # Link to full product page

class ProductAdmin(admin.ModelAdmin):
    list_display = ['name', 'category', 'price', 'is_active']
    list_filter = ['category', 'is_active']
    search_fields = ['name', 'description']
    
    # Add inline images
    inlines = [ProductImageInline]
    
    fieldsets = (
        ('Basic Info', {
            'fields': ('name', 'category', 'description')
        }),
        ('Pricing', {
            'fields': ('price', 'is_active')
        }),
    )

class CategoryAdmin(admin.ModelAdmin):
    list_display = ['name', 'product_count']
    search_fields = ['name']
    
    # Show products within category
    inlines = [ProductInline]
    
    # Custom method: Count products
    def product_count(self, obj):
        return obj.product_set.count()
    product_count.short_description = 'Products'

admin.site.register(Category, CategoryAdmin)
admin.site.register(Product, ProductAdmin)
```

**Result:** Edit product images directly on product page, or edit products while editing category!

---

### Step 9: Customizing the Admin Site

```python
# admin.py
from django.contrib import admin

# Customize admin site header and title
admin.site.site_header = 'My Store Administration'
admin.site.site_title = 'My Store Admin'
admin.site.index_title = 'Welcome to My Store Admin Panel'

# Custom admin site
class MyAdminSite(admin.AdminSite):
    site_header = 'Custom Admin'
    site_title = 'Custom Admin Portal'
    index_title = 'Welcome to Custom Admin'

# Create instance
# admin_site = MyAdminSite(name='myadmin')
# Then use admin_site.register() instead of admin.site.register()
```

---

## 🎯 Complete Admin Example

```python
# products/models.py
from django.db import models
from django.utils.text import slugify

class Category(models.Model):
    name = models.CharField(max_length=100)
    slug = models.SlugField(unique=True)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.name
    
    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(self.name)
        super().save(*args, **kwargs)
    
    class Meta:
        verbose_name_plural = 'Categories'
        ordering = ['name']

class Product(models.Model):
    STATUS_CHOICES = [
        ('draft', 'Draft'),
        ('active', 'Active'),
        ('archived', 'Archived'),
    ]
    
    category = models.ForeignKey(Category, on_delete=models.CASCADE)
    name = models.CharField(max_length=200)
    slug = models.SlugField(unique=True)
    description = models.TextField(blank=True)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    cost = models.DecimalField(max_digits=10, decimal_places=2, default=0)
    stock_quantity = models.IntegerField(default=0)
    status = models.CharField(max_length=10, choices=STATUS_CHOICES, default='draft')
    is_featured = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.name
    
    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(self.name)
        super().save(*args, **kwargs)
    
    @property
    def profit_margin(self):
        if self.cost > 0:
            return ((self.price - self.cost) / self.cost) * 100
        return 0
    
    class Meta:
        ordering = ['-created_at']

class ProductImage(models.Model):
    product = models.ForeignKey(Product, on_delete=models.CASCADE, related_name='images')
    image = models.ImageField(upload_to='products/%Y/%m/')
    caption = models.CharField(max_length=200, blank=True)
    is_primary = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return f"{self.product.name} - {self.caption or 'Image'}"
    
    class Meta:
        ordering = ['-is_primary', '-created_at']
```

```python
# products/admin.py
from django.contrib import admin
from django.utils.html import format_html
from django.db.models import Sum, Count, Avg
from django.urls import reverse
from django.utils.safestring import mark_safe
from .models import Category, Product, ProductImage

# ===== FILTERS =====

class StockFilter(admin.SimpleListFilter):
    title = 'stock status'
    parameter_name = 'stock'
    
    def lookups(self, request, model_admin):
        return (
            ('in_stock', 'In Stock (10+)'),
            ('low_stock', 'Low Stock (1-9)'),
            ('out', 'Out of Stock'),
        )
    
    def queryset(self, request, queryset):
        if self.value() == 'in_stock':
            return queryset.filter(stock_quantity__gte=10)
        if self.value() == 'low_stock':
            return queryset.filter(stock_quantity__gt=0, stock_quantity__lt=10)
        if self.value() == 'out':
            return queryset.filter(stock_quantity=0)

class PriceRangeFilter(admin.SimpleListFilter):
    title = 'price range'
    parameter_name = 'price_range'
    
    def lookups(self, request, model_admin):
        return (
            ('0-50', '$0 - $50'),
            ('50-100', '$50 - $100'),
            ('100-500', '$100 - $500'),
            ('500+', '$500+'),
        )
    
    def queryset(self, request, queryset):
        if self.value() == '0-50':
            return queryset.filter(price__lt=50)
        if self.value() == '50-100':
            return queryset.filter(price__gte=50, price__lt=100)
        if self.value() == '100-500':
            return queryset.filter(price__gte=100, price__lt=500)
        if self.value() == '500+':
            return queryset.filter(price__gte=500)

# ===== INLINES =====

class ProductImageInline(admin.TabularInline):
    model = ProductImage
    extra = 1
    fields = ['image', 'caption', 'is_primary', 'image_preview']
    readonly_fields = ['image_preview']
    
    def image_preview(self, obj):
        if obj.image:
            return mark_safe(f'<img src="{obj.image.url}" width="100" />')
        return "No image"
    image_preview.short_description = 'Preview'

class ProductInline(admin.TabularInline):
    model = Product
    extra = 0
    fields = ['name', 'price', 'stock_quantity', 'status']
    readonly_fields = []
    show_change_link = True

# ===== CATEGORY ADMIN =====

@admin.register(Category)
class CategoryAdmin(admin.ModelAdmin):
    list_display = ['name', 'product_count', 'total_stock_value', 'created_at']
    search_fields = ['name', 'description']
    prepopulated_fields = {'slug': ('name',)}
    
    inlines = [ProductInline]
    
    fieldsets = (
        ('Category Information', {
            'fields': ('name', 'slug', 'description')
        }),
    )
    
    def product_count(self, obj):
        count = obj.product_set.count()
        url = reverse('admin:products_product_changelist') + f'?category__id__exact={obj.id}'
        return format_html('<a href="{}">{} products</a>', url, count)
    product_count.short_description = 'Products'
    
    def total_stock_value(self, obj):
        total = obj.product_set.aggregate(
            total=Sum('price')
        )['total'] or 0
        return f"${total:.2f}"
    total_stock_value.short_description = 'Total Value'

# ===== PRODUCT ADMIN =====

@admin.register(Product)
class ProductAdmin(admin.ModelAdmin):
    list_display = [
        'name',
        'category',
        'formatted_price',
        'formatted_cost',
        'profit_margin_display',
        'stock_status',
        'status_colored',
        'is_featured',
        'created_at'
    ]
    
    list_display_links = ['name']
    list_editable = ['is_featured']
    
    list_filter = [
        'category',
        'status',
        'is_featured',
        StockFilter,
        PriceRangeFilter,
        'created_at',
    ]
    
    search_fields = ['name', 'description', 'slug']
    
    prepopulated_fields = {'slug': ('name',)}
    
    date_hierarchy = 'created_at'
    
    list_per_page = 25
    
    ordering = ['-created_at']
    
    actions = [
        'activate_products',
        'archive_products',
        'mark_as_featured',
        'apply_discount',
        'restock',
    ]
    
    inlines = [ProductImageInline]
    
    fieldsets = (
        ('Basic Information', {
            'fields': ('name', 'slug', 'category', 'description')
        }),
        ('Pricing', {
            'fields': ('cost', 'price'),
            'description': 'Set cost and selling price'
        }),
        ('Inventory', {
            'fields': ('stock_quantity',)
        }),
        ('Status', {
            'fields': ('status', 'is_featured')
        }),
        ('Timestamps', {
            'fields': ('created_at', 'updated_at'),
            'classes': ('collapse',)
        }),
    )
    
    readonly_fields = ['created_at', 'updated_at']
    
    # ===== CUSTOM DISPLAY METHODS =====
    
    def formatted_price(self, obj):
        return f"${obj.price:.2f}"
    formatted_price.short_description = 'Price'
    formatted_price.admin_order_field = 'price'
    
    def formatted_cost(self, obj):
        return f"${obj.cost:.2f}"
    formatted_cost.short_description = 'Cost'
    formatted_cost.admin_order_field = 'cost'
    
    def profit_margin_display(self, obj):
        margin = obj.profit_margin
        if margin > 50:
            color = 'green'
        elif margin > 20:
            color = 'orange'
        else:
            color = 'red'
        return format_html(
            '<span style="color: {};">{:.1f}%</span>',
            color,
            margin
        )
    profit_margin_display.short_description = 'Profit'
    
    def stock_status(self, obj):
        if obj.stock_quantity == 0:
            return format_html(
                '<span style="color: red; font-weight: bold;">OUT OF STOCK</span>'
            )
        elif obj.stock_quantity < 10:
            return format_html(
                '<span style="color: orange;">Low ({} left)</span>',
                obj.stock_quantity
            )
        else:
            return format_html(
                '<span style="color: green;">In Stock ({})</span>',
                obj.stock_quantity
            )
    stock_status.short_description = 'Stock'
    stock_status.admin_order_field = 'stock_quantity'
    
    def status_colored(self, obj):
        colors = {
            'draft': 'gray',
            'active': 'green',
            'archived': 'red',
        }
        return format_html(
            '<span style="color: {};">●</span> {}',
            colors.get(obj.status, 'black'),
            obj.get_status_display()
        )
    status_colored.short_description = 'Status'
    status_colored.admin_order_field = 'status'
    
    # ===== CUSTOM ACTIONS =====
    
    def activate_products(self, request, queryset):
        updated = queryset.update(status='active')
        self.message_user(request, f'{updated} products activated.', 'success')
    activate_products.short_description = 'Activate selected products'
    
    def archive_products(self, request, queryset):
        updated = queryset.update(status='archived')
        self.message_user(request, f'{updated} products archived.', 'warning')
    archive_products.short_description = 'Archive selected products'
    
    def mark_as_featured(self, request, queryset):
        updated = queryset.update(is_featured=True)
        self.message_user(request, f'{updated} products marked as featured.', 'success')
    mark_as_featured.short_description = 'Mark as featured'
    
    def apply_discount(self, request, queryset):
        from django.db.models import F
        updated = queryset.update(price=F('price') * 0.9)
        self.message_user(request, f'Applied 10% discount to {updated} products.', 'success')
    apply_discount.short_description = 'Apply 10% discount'
    
    def restock(self, request, queryset):
        from django.db.models import F
        updated = queryset.update(stock_quantity=F('stock_quantity') + 100)
        self.message_user(request, f'Added 100 units to {updated} products.', 'success')
    restock.short_description = 'Add 100 units to stock'

# ===== PRODUCT IMAGE ADMIN =====

@admin.register(ProductImage)
class ProductImageAdmin(admin.ModelAdmin):
    list_display = ['product', 'caption', 'is_primary', 'image_preview', 'created_at']
    list_filter = ['is_primary', 'created_at']
    search_fields = ['product__name', 'caption']
    
    def image_preview(self, obj):
        if obj.image:
            return mark_safe(f'<img src="{obj.image.url}" width="100" />')
        return "No image"
    image_preview.short_description = 'Preview'

# Customize admin site
admin.site.site_header = 'Product Management System'
admin.site.site_title = 'Product Admin'
admin.site.index_title = 'Welcome to Product Administration'
```

---

## 💡 Best Practices

### ✅ DO:

1. **Add `__str__` methods** to all models for better display
2. **Use list_display** to show important fields
3. **Add search_fields** for searchable models
4. **Use list_filter** for common filters
5. **Organize with fieldsets** for complex forms
6. **Add custom display methods** for calculated fields
7. **Create custom bulk actions** for common tasks
8. **Use inlines** for related models
9. **Add readonly_fields** for timestamps and auto-generated fields
10. **Customize admin for better UX**

### ❌ DON'T:

1. **Don't expose admin to public** - Use permissions!
2. **Don't skip `__str__` methods** - Makes debugging hard
3. **Don't make everything editable** - Use readonly_fields
4. **Don't forget to register models**
5. **Don't use admin for complex public forms**

---

## ✏️ Practice Exercise

### Exercise 2.7: Complete Admin Interface

**Task:** Create a comprehensive admin interface for a book management system.

```python
# books/models.py
class Author(models.Model):
    name = models.CharField(max_length=100)
    bio = models.TextField(blank=True)
    birth_date = models.DateField(null=True, blank=True)
    
    def __str__(self):
        return self.name

class Publisher(models.Model):
    name = models.CharField(max_length=100)
    website = models.URLField(blank=True)
    
    def __str__(self):
        return self.name

class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.ForeignKey(Author, on_delete=models.CASCADE)
    publisher = models.ForeignKey(Publisher, on_delete=models.CASCADE)
    isbn = models.CharField(max_length=13, unique=True)
    publication_date = models.DateField()
    pages = models.PositiveIntegerField()
    price = models.DecimalField(max_digits=6, decimal_places=2)
    stock = models.PositiveIntegerField(default=0)
    is_bestseller = models.BooleanField(default=False)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.title
```

**Requirements:**

1. **Author Admin:**
   - List: name, book_count, birth_date
   - Search: name
   - Filter: birth_date (year)
   - Inline: books

2. **Publisher Admin:**
   - List: name, book_count, website
   - Search: name
   - Inline: books

3. **Book Admin:**
   - List: title, author, publisher, formatted_price, stock_status, is_bestseller
   - Search: title, isbn, author name
   - Filter: author, publisher, is_bestseller, publication_date
   - Custom filters: price_range, stock_status
   - Fieldsets: organized sections
   - Actions: mark_bestseller, apply_discount, restock
   - Custom methods: stock_status, formatted_price

**Bonus:**
- Add colored status indicators
- Add custom filters
- Add bulk actions
- Add statistics in list display

---

## 🎓 Key Takeaways

1. ✅ Django Admin provides instant CRUD interface
2. ✅ Register models with `admin.site.register()`
3. ✅ Customize with ModelAdmin classes
4. ✅ Use list_display, list_filter, search_fields
5. ✅ Organize forms with fieldsets
6. ✅ Add custom display methods for calculated fields
7. ✅ Create bulk actions for common operations
8. ✅ Use inlines for related models
9. ✅ Customize appearance with format_html
10. ✅ Always add `__str__` methods to models

---

## 🔗 Additional Resources

- [Django Admin Documentation](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/)
- [ModelAdmin Options](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/#modeladmin-options)
- [Admin Actions](https://docs.djangoproject.com/en/4.2/ref/contrib/admin/actions/)

---

[← Previous: Django ORM & QuerySets](./04-orm-querysets.md) | [Back to Part 2](./README.md)
