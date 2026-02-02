# Migrations: makemigrations & migrate

## 📋 Table of Contents
- [WHY - Why Use Migrations?](#why---why-use-migrations)
- [WHEN - When to Use Migrations?](#when---when-to-use-migrations)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use Migrations?

Migrations are Django's way of propagating changes you make to your models (adding a field, deleting a model, etc.) into your database schema. They are version control for your database.

### 🎭 Real-Life Analogy: Building Blueprints

Imagine constructing a building:
- **Without Migrations**: Every time you want to change the building, you manually tell workers what to modify. If something goes wrong, you can't undo it easily. Different workers might make different changes.
- **With Migrations**: You create detailed blueprints (migration files) for every change. You can see the history of all changes, undo them, and ensure everyone follows the same instructions.

### Benefits of Migrations:

- ✅ **Version Control**: Track all database schema changes over time
- ✅ **Reproducibility**: Same changes apply consistently across environments
- ✅ **Reversibility**: Roll back changes if something goes wrong
- ✅ **Team Collaboration**: Share database changes with your team
- ✅ **Database Agnostic**: Works with SQLite, PostgreSQL, MySQL, etc.
- ✅ **Safety**: Preview changes before applying them
- ✅ **Automation**: Django generates migration files automatically

---

## 2️⃣ WHEN - When to Use Migrations?

### ✅ Run Migrations When You:

- Create a new model
- Add, remove, or modify a field
- Change field options (max_length, default, etc.)
- Add or remove indexes
- Change Meta options
- Rename models or fields
- Set up a new environment (development, staging, production)
- Pull changes from version control that include migrations

### The Migration Workflow:

```
1. Modify models.py
2. Run makemigrations → Creates migration file
3. Review migration file → Check what will happen
4. Run migrate → Apply changes to database
5. Commit migration file → Share with team
```

### ❌ Don't Create Migrations For:

- Changes to views, templates, or URLs
- Changes to model methods (functions)
- Changes to properties
- Documentation changes

---

## 3️⃣ HOW - Implementation

### Step 1: Understanding Migration Commands

```bash
# Create migration files (detects model changes)
python manage.py makemigrations

# Apply migrations to database
python manage.py migrate

# View SQL that will be executed (preview)
python manage.py sqlmigrate app_name migration_name

# Show migration status
python manage.py showmigrations

# Create empty migration (for custom operations)
python manage.py makemigrations app_name --empty

# Fake a migration (mark as applied without running)
python manage.py migrate app_name migration_name --fake
```

---

### Step 2: Your First Migration

**1. Create a Model:**

```python
# products/models.py
from django.db import models

class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.name
```

**2. Run makemigrations:**

```bash
python manage.py makemigrations
```

**Output:**
```
Migrations for 'products':
  products/migrations/0001_initial.py
    - Create model Product
```

**3. Check the Migration File:**

```python
# products/migrations/0001_initial.py
from django.db import migrations, models

class Migration(migrations.Migration):

    initial = True

    dependencies = []

    operations = [
        migrations.CreateModel(
            name='Product',
            fields=[
                ('id', models.BigAutoField(auto_created=True, primary_key=True, serialize=False, verbose_name='ID')),
                ('name', models.CharField(max_length=200)),
                ('price', models.DecimalField(decimal_places=2, max_digits=10)),
                ('created_at', models.DateTimeField(auto_now_add=True)),
            ],
        ),
    ]
```

**4. Preview SQL (Optional):**

```bash
python manage.py sqlmigrate products 0001
```

**Output:**
```sql
BEGIN;
--
-- Create model Product
--
CREATE TABLE "products_product" (
    "id" integer NOT NULL PRIMARY KEY AUTOINCREMENT,
    "name" varchar(200) NOT NULL,
    "price" decimal NOT NULL,
    "created_at" datetime NOT NULL
);
COMMIT;
```

**5. Apply Migration:**

```bash
python manage.py migrate
```

**Output:**
```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, products, sessions
Running migrations:
  Applying products.0001_initial... OK
```

🎉 **Your database table is now created!**

---

### Step 3: Adding Fields (Making Changes)

**Scenario:** Add description and stock_quantity fields to Product.

**1. Modify the Model:**

```python
# products/models.py
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField(blank=True)  # New field
    stock_quantity = models.IntegerField(default=0)  # New field
    created_at = models.DateTimeField(auto_now_add=True)
```

**2. Create Migration:**

```bash
python manage.py makemigrations
```

**Output:**
```
Migrations for 'products':
  products/migrations/0002_product_description_product_stock_quantity.py
    - Add field description to product
    - Add field stock_quantity to product
```

**3. Review Migration File:**

```python
# products/migrations/0002_product_description_product_stock_quantity.py
from django.db import migrations, models

class Migration(migrations.Migration):

    dependencies = [
        ('products', '0001_initial'),  # Depends on previous migration
    ]

    operations = [
        migrations.AddField(
            model_name='product',
            name='description',
            field=models.TextField(blank=True),
        ),
        migrations.AddField(
            model_name='product',
            name='stock_quantity',
            field=models.IntegerField(default=0),
        ),
    ]
```

**4. Apply Migration:**

```bash
python manage.py migrate
```

**Output:**
```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, products, sessions
Running migrations:
  Applying products.0002_product_description_product_stock_quantity... OK
```

---

### Step 4: Handling Non-Nullable Fields

**Problem:** What if you add a required field to a model with existing data?

**Scenario:** Add a required `sku` field:

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    sku = models.CharField(max_length=50, unique=True)  # No default!
    price = models.DecimalField(max_digits=10, decimal_places=2)
    # ... other fields
```

**Run makemigrations:**

```bash
python manage.py makemigrations
```

**Django Prompts You:**
```
You are trying to add a non-nullable field 'sku' to product without a default; 
we can't do that (the database needs something to populate existing rows).
Please select a fix:
 1) Provide a one-off default now (will be set on all existing rows with a null value for this column)
 2) Quit, and let me add a default in models.py
Select an option:
```

**Option 1: Provide One-Off Default**
```
Select an option: 1
Please enter the default value now, as valid Python
The datetime and django.utils.timezone modules are available, so you can do e.g. timezone.now
Type 'exit' to exit this prompt
>>> 'TEMP-SKU'
```

**Option 2: Add Default in models.py**
```python
sku = models.CharField(max_length=50, unique=True, default='UNKNOWN')
```

**Best Practice for Production:**

```python
# Step 1: Add field as nullable first
sku = models.CharField(max_length=50, unique=True, null=True, blank=True)
# Run makemigrations and migrate

# Step 2: Populate data programmatically
from products.models import Product
for i, product in enumerate(Product.objects.filter(sku__isnull=True), 1):
    product.sku = f'SKU-{i:05d}'
    product.save()

# Step 3: Remove null=True, blank=True
sku = models.CharField(max_length=50, unique=True)
# Run makemigrations and migrate again
```

---

### Step 5: Removing Fields

**1. Remove Field from Model:**

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    # description field removed
    price = models.DecimalField(max_digits=10, decimal_places=2)
```

**2. Create Migration:**

```bash
python manage.py makemigrations
```

**Output:**
```
Migrations for 'products':
  products/migrations/0003_remove_product_description.py
    - Remove field description from product
```

**⚠️ Warning: This will delete all data in that column!**

**3. Apply Migration:**

```bash
python manage.py migrate
```

---

### Step 6: Renaming Fields

**Wrong Way (Creates Delete + Add):**
```python
# Old
name = models.CharField(max_length=200)

# New
title = models.CharField(max_length=200)
# makemigrations will DELETE name and ADD title (data lost!)
```

**Right Way (Use RenameField):**

**1. Run makemigrations with --name flag:**

```bash
python manage.py makemigrations products --name rename_name_to_title
```

**2. Django will ask:**
```
Did you rename product.name to product.title (a CharField)? [y/N] y
```

**3. Migration File:**
```python
from django.db import migrations

class Migration(migrations.Migration):
    operations = [
        migrations.RenameField(
            model_name='product',
            old_name='name',
            new_name='title',
        ),
    ]
```

**Manual RenameField:**
```python
# In migration file
operations = [
    migrations.RenameField(
        model_name='product',
        old_name='name',
        new_name='title',
    ),
]
```

---

### Step 7: Checking Migration Status

```bash
# Show all migrations and their status
python manage.py showmigrations
```

**Output:**
```
admin
 [X] 0001_initial
 [X] 0002_logentry_remove_auto_add
auth
 [X] 0001_initial
 [X] 0002_alter_permission_name_max_length
products
 [X] 0001_initial
 [X] 0002_product_description_product_stock_quantity
 [ ] 0003_remove_product_description  # Not applied yet
```

Legend:
- `[X]` = Applied
- `[ ]` = Not applied

**Check specific app:**
```bash
python manage.py showmigrations products
```

---

### Step 8: Rolling Back Migrations

**Scenario:** You applied a migration but want to undo it.

**Current State:**
```
products
 [X] 0001_initial
 [X] 0002_add_fields
 [X] 0003_remove_description  ← Want to undo this
```

**Rollback to 0002:**
```bash
python manage.py migrate products 0002
```

**Output:**
```
Operations to perform:
  Target specific migration: 0002_add_fields, from products
Running migrations:
  Rendering model states... DONE
  Unapplying products.0003_remove_description... OK
```

**Rollback all migrations in app:**
```bash
python manage.py migrate products zero
```

---

### Step 9: Squashing Migrations

**Problem:** Too many migration files accumulate over time.

**Solution:** Squash multiple migrations into one.

**Current State:**
```
products/migrations/
├── 0001_initial.py
├── 0002_add_description.py
├── 0003_add_stock.py
├── 0004_add_sku.py
├── 0005_add_category.py
```

**Squash Migrations:**
```bash
python manage.py squashmigrations products 0001 0005
```

**Creates:**
```
products/migrations/
├── 0001_squashed_0005_auto_YYYYMMDD_HHMM.py  # Squashed migration
├── 0001_initial.py  # Keep for existing databases
├── 0002_add_description.py
├── ...
```

**After all databases use squashed migration, delete old ones.**

---

### Step 10: Data Migrations

**Scenario:** You need to modify data during migration, not just schema.

**Example: Populate slugs for existing products**

**Create Empty Migration:**
```bash
python manage.py makemigrations products --empty --name populate_slugs
```

**Edit Migration File:**
```python
# products/migrations/0006_populate_slugs.py
from django.db import migrations
from django.utils.text import slugify

def populate_slugs(apps, schema_editor):
    """
    Populate slug field for all existing products.
    """
    # Get model from historical state
    Product = apps.get_model('products', 'Product')
    
    for product in Product.objects.all():
        if not product.slug:
            product.slug = slugify(product.name)
            product.save()

def reverse_populate_slugs(apps, schema_editor):
    """
    Clear slugs (reverse operation).
    """
    Product = apps.get_model('products', 'Product')
    Product.objects.all().update(slug='')

class Migration(migrations.Migration):

    dependencies = [
        ('products', '0005_product_slug'),
    ]

    operations = [
        migrations.RunPython(
            populate_slugs,
            reverse_code=reverse_populate_slugs
        ),
    ]
```

**Apply Migration:**
```bash
python manage.py migrate
```

---

## 🔄 Complete Migration Workflow Example

**Scenario:** Building an e-commerce product catalog from scratch.

### Migration 1: Initial Model

```python
# products/models.py
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    created_at = models.DateTimeField(auto_now_add=True)
```

```bash
python manage.py makemigrations
python manage.py migrate
```

### Migration 2: Add More Fields

```python
class Product(models.Model):
    name = models.CharField(max_length=200)
    price = models.DecimalField(max_digits=10, decimal_places=2)
    description = models.TextField(blank=True)  # Added
    stock_quantity = models.IntegerField(default=0)  # Added
    is_active = models.BooleanField(default=True)  # Added
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)  # Added
```

```bash
python manage.py makemigrations
python manage.py migrate
```

### Migration 3: Add SKU with Safe Approach

```python
class Product(models.Model):
    # ... existing fields
    sku = models.CharField(max_length=50, null=True, blank=True)  # Nullable first
```

```bash
python manage.py makemigrations
python manage.py migrate

# Populate SKUs
python manage.py shell
>>> from products.models import Product
>>> for i, p in enumerate(Product.objects.all(), 1):
...     p.sku = f'SKU-{i:05d}'
...     p.save()
>>> exit()
```

### Migration 4: Make SKU Required

```python
class Product(models.Model):
    # ... existing fields
    sku = models.CharField(max_length=50, unique=True)  # Now required and unique
```

```bash
python manage.py makemigrations
python manage.py migrate
```

### Migration 5: Add Slug Field with Data Migration

```python
class Product(models.Model):
    # ... existing fields
    slug = models.SlugField(max_length=200, unique=True, null=True)
```

```bash
python manage.py makemigrations
python manage.py migrate

# Create data migration
python manage.py makemigrations products --empty --name populate_slugs
# Edit migration file to populate slugs
python manage.py migrate
```

### Migration 6: Make Slug Required

```python
class Product(models.Model):
    # ... existing fields
    slug = models.SlugField(max_length=200, unique=True)  # Remove null=True
```

```bash
python manage.py makemigrations
python manage.py migrate
```

---

## 🐛 Common Migration Issues & Solutions

### Issue 1: Migration Conflicts

**Problem:**
```
CommandError: Conflicting migrations detected; multiple leaf nodes in the migration graph
```

**Cause:** Two branches of migrations exist (often from merging git branches).

**Solution:**
```bash
python manage.py makemigrations --merge
python manage.py migrate
```

---

### Issue 2: Fake Migrations

**Scenario:** Database already has changes but no migration file.

**Solution:**
```bash
# Mark migration as applied without running it
python manage.py migrate products 0001 --fake
```

---

### Issue 3: Resetting Migrations

**Scenario:** Development database is messy; start fresh.

**⚠️ ONLY for development! This deletes all data!**

```bash
# 1. Delete database
rm db.sqlite3

# 2. Delete migration files (keep __init__.py)
rm products/migrations/0*.py

# 3. Recreate migrations
python manage.py makemigrations

# 4. Create database
python manage.py migrate

# 5. Create superuser
python manage.py createsuperuser
```

---

### Issue 4: Migration Doesn't Detect Changes

**Problem:** Changed model but makemigrations says "No changes detected".

**Solutions:**

1. **Check app is in INSTALLED_APPS:**
```python
# settings.py
INSTALLED_APPS = [
    # ...
    'products',  # Make sure this is here!
]
```

2. **Specify app name:**
```bash
python manage.py makemigrations products
```

3. **Check for syntax errors:**
```bash
python manage.py check
```

---

## 💡 Best Practices

### ✅ DO:

1. **Always run makemigrations after model changes**
2. **Review migration files before applying**
3. **Commit migration files to version control**
4. **Run migrations in order: local → staging → production**
5. **Backup database before migrations in production**
6. **Test migrations on a copy of production data**
7. **Use data migrations for complex data transformations**
8. **Squash old migrations periodically**

### ❌ DON'T:

1. **Don't edit applied migrations** (create new ones instead)
2. **Don't delete migration files** (unless you know what you're doing)
3. **Don't commit broken migrations**
4. **Don't apply migrations without reviewing them first**
5. **Don't skip migrations** (apply in order)
6. **Don't share databases between developers** (use migrations)

---

## ✏️ Practice Exercise

### Exercise 2.3: Complete Migration Workflow

**Task:** Build a Book model through multiple migrations.

**Step 1: Initial Model**
```python
# books/models.py
class Book(models.Model):
    title = models.CharField(max_length=200)
    author = models.CharField(max_length=100)
    published_date = models.DateField()
    
    def __str__(self):
        return self.title
```
- Create and apply migration

**Step 2: Add Fields**
Add these fields:
- `isbn` (CharField, 13 chars)
- `pages` (PositiveIntegerField)
- `price` (DecimalField)
- `created_at` (auto timestamp)

- Create and apply migration

**Step 3: Add Nullable Fields**
Add:
- `description` (TextField, optional)
- `cover_image` (ImageField, optional)

- Create and apply migration

**Step 4: Add Required Field Safely**
Add `slug` field in 3 migrations:
1. Add as nullable
2. Populate data
3. Make required

**Step 5: Add Choices**
Add `status` field with choices:
- draft
- published
- archived

- Create and apply migration

**Expected Results:**
```bash
python manage.py showmigrations books
# Should show 5+ migrations all applied

python manage.py shell
>>> from books.models import Book
>>> Book.objects.create(
...     title="Python Crash Course",
...     author="Eric Matthes",
...     published_date="2023-01-15",
...     isbn="9781593279288",
...     pages=544,
...     price=39.99,
...     slug="python-crash-course",
...     status="published"
... )
```

---

### Exercise 2.4: Rollback and Fix

**Scenario:** You applied a bad migration.

**Tasks:**
1. Create a migration that removes an important field
2. Apply it
3. Realize the mistake
4. Rollback the migration
5. Fix the model
6. Create correct migration

---

## 🎓 Key Takeaways

1. ✅ Migrations track database schema changes
2. ✅ Use `makemigrations` to create, `migrate` to apply
3. ✅ Always review migration files before applying
4. ✅ Add required fields safely: nullable → populate → required
5. ✅ Use RenameField to rename without data loss
6. ✅ Data migrations for populating or transforming data
7. ✅ Commit migration files to version control
8. ✅ Test migrations on copy of production data

---

## 🔗 Additional Resources

- [Django Migrations Documentation](https://docs.djangoproject.com/en/4.2/topics/migrations/)
- [Migration Operations Reference](https://docs.djangoproject.com/en/4.2/ref/migration-operations/)
- [Data Migrations](https://docs.djangoproject.com/en/4.2/topics/migrations/#data-migrations)

---

[← Previous: Field Types](./02-field-types.md) | [Next: Django ORM & QuerySets →](./04-orm-querysets.md)
