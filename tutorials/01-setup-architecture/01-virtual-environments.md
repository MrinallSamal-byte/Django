# Virtual Environments & Django Installation

## 📋 Table of Contents
- [WHY - Why Use Virtual Environments?](#why---why-use-virtual-environments)
- [WHEN - When to Use Virtual Environments?](#when---when-to-use-virtual-environments)
- [HOW - Implementation](#how---implementation)
- [Practice Exercise](#practice-exercise)

---

## 1️⃣ WHY - Why Use Virtual Environments?

Virtual environments are isolated Python environments that keep project dependencies separate from your system Python installation. This prevents conflicts between different projects that might require different versions of the same package.

### 🎭 Real-Life Analogy: The Toolbox
Imagine you're a carpenter working on multiple projects:
- **Project A** (antique furniture): Requires old, traditional tools
- **Project B** (modern furniture): Requires new, power tools

You wouldn't want to mix all tools in one toolbox! Similarly, virtual environments keep project dependencies organized and isolated.

### Benefits:
- ✅ **Dependency Isolation**: Each project has its own packages
- ✅ **Version Control**: Different projects can use different Django versions
- ✅ **Clean System**: Your system Python remains untouched
- ✅ **Reproducibility**: Easy to recreate the exact environment
- ✅ **No Permission Issues**: No need for sudo/admin rights

---

## 2️⃣ WHEN - When to Use Virtual Environments?

### Always Use Virtual Environments When:
- ✅ Starting a new Django project
- ✅ Working on multiple Python projects
- ✅ Testing different package versions
- ✅ Collaborating with a team
- ✅ Deploying to production

### Exception (rarely):
- ❌ One-off scripts that don't need packages
- ❌ System-wide tools (use pipx instead)

---

## 3️⃣ HOW - Implementation

### Step 1: Check Python Installation

```bash
# Check Python version (3.8+ required)
python --version
# or
python3 --version
```

**Expected Output:**
```
Python 3.11.4
```

---

### Step 2: Create a Virtual Environment

#### On Windows:
```bash
# Navigate to your project directory
cd C:\projects\my_django_project

# Create virtual environment named 'venv'
python -m venv venv
```

#### On macOS/Linux:
```bash
# Navigate to your project directory
cd ~/projects/my_django_project

# Create virtual environment named 'venv'
python3 -m venv venv
```

**What happens here?**
- `python -m venv`: Runs the venv module
- `venv`: Name of the virtual environment folder (can be anything)

**Directory structure created:**
```
my_django_project/
└── venv/
    ├── bin/         # (Scripts/ on Windows) - executables
    ├── include/     # C headers
    ├── lib/         # Installed packages
    └── pyvenv.cfg   # Configuration
```

---

### Step 3: Activate the Virtual Environment

#### On Windows (Command Prompt):
```bash
venv\Scripts\activate
```

#### On Windows (PowerShell):
```bash
venv\Scripts\Activate.ps1
```

#### On macOS/Linux:
```bash
source venv/bin/activate
```

**How to know it's activated?**
Your terminal prompt will show `(venv)`:
```bash
(venv) C:\projects\my_django_project>
```

---

### Step 4: Install Django

```bash
# With virtual environment activated
pip install django

# Install a specific version
pip install django==4.2

# Verify installation
python -m django --version
```

**Expected Output:**
```
4.2.7
```

---

### Step 5: Verify Django Installation

```bash
# Check installed packages
pip list
```

**Expected Output:**
```
Package    Version
---------- -------
asgiref    3.7.2
Django     4.2.7
pip        23.3.1
sqlparse   0.4.4
tzdata     2023.3
```

---

### Step 6: Create requirements.txt

```bash
# Save installed packages to requirements.txt
pip freeze > requirements.txt
```

**requirements.txt content:**
```
asgiref==3.7.2
Django==4.2.7
sqlparse==0.4.4
tzdata==2023.3
```

**Why is this important?**
- ✅ Share exact dependency versions with your team
- ✅ Recreate the environment on another machine
- ✅ Deploy to production with confidence

---

### Step 7: Deactivate Virtual Environment

```bash
# When you're done working
deactivate
```

Your prompt returns to normal:
```bash
C:\projects\my_django_project>
```

---

## 🔄 Recreating the Environment

On a new machine or for a team member:

```bash
# 1. Create virtual environment
python -m venv venv

# 2. Activate it
source venv/bin/activate  # or venv\Scripts\activate on Windows

# 3. Install dependencies
pip install -r requirements.txt

# 4. Verify
python -m django --version
```

---

## 🎯 Complete Example

Let's walk through a complete setup:

```bash
# 1. Create project directory
mkdir my_first_django_app
cd my_first_django_app

# 2. Create virtual environment
python -m venv venv

# 3. Activate virtual environment
source venv/bin/activate  # Windows: venv\Scripts\activate

# 4. Upgrade pip (recommended)
pip install --upgrade pip

# 5. Install Django
pip install django

# 6. Verify installation
python -m django --version

# 7. Save dependencies
pip freeze > requirements.txt

# 8. Show installed packages
pip list
```

**Complete Terminal Output:**
```bash
$ mkdir my_first_django_app
$ cd my_first_django_app
$ python3 -m venv venv
$ source venv/bin/activate
(venv) $ pip install --upgrade pip
Successfully installed pip-23.3.1
(venv) $ pip install django
Successfully installed Django-4.2.7 asgiref-3.7.2 sqlparse-0.4.4
(venv) $ python -m django --version
4.2.7
(venv) $ pip freeze > requirements.txt
(venv) $ cat requirements.txt
asgiref==3.7.2
Django==4.2.7
sqlparse==0.4.4
```

---

## 🐛 Common Issues & Solutions

### Issue 1: "python: command not found"
**Solution:**
```bash
# Try python3 instead
python3 -m venv venv
```

### Issue 2: PowerShell Script Execution Error (Windows)
```
venv\Scripts\Activate.ps1 cannot be loaded because running scripts is disabled
```

**Solution:**
```powershell
# Run PowerShell as Administrator
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Then activate
venv\Scripts\Activate.ps1
```

### Issue 3: Permission Denied (macOS/Linux)
```bash
# Make sure you have write permissions
ls -la

# If needed, take ownership
sudo chown -R $USER:$USER .
```

### Issue 4: Virtual Environment Already Exists
```bash
# Remove existing venv
rm -rf venv  # Linux/macOS
rmdir /s venv  # Windows

# Create new one
python -m venv venv
```

---

## 💡 Best Practices

### ✅ DO:
1. **Name consistently**: Use `venv` or `.venv` for all projects
2. **Activate first**: Always activate before installing packages
3. **Use requirements.txt**: Track dependencies
4. **Add to .gitignore**: Don't commit virtual environments
5. **Update regularly**: Keep packages updated

### ❌ DON'T:
1. **Don't commit venv**: Add to `.gitignore`
2. **Don't install globally**: Always use virtual environment
3. **Don't mix environments**: One project = one venv
4. **Don't forget to activate**: Check for `(venv)` in prompt

---

## 📝 .gitignore Template

Create a `.gitignore` file in your project root:

```gitignore
# Virtual Environment
venv/
env/
.venv/

# Django
*.pyc
__pycache__/
db.sqlite3
media/
staticfiles/

# IDE
.vscode/
.idea/
*.swp

# OS
.DS_Store
Thumbs.db
```

---

## ✏️ Practice Exercise

### Exercise 1.1: Your First Virtual Environment

**Task:**
Create a Django project setup with proper virtual environment and dependency management.

**Steps:**
1. Create a folder named `blog_project`
2. Create and activate a virtual environment
3. Install Django 4.2
4. Create a `requirements.txt` file
5. Verify Django installation by checking the version
6. Create a `.gitignore` file with proper exclusions

**Expected Result:**
```
blog_project/
├── venv/                    # Virtual environment (not in git)
├── requirements.txt         # Django==4.2.7
└── .gitignore              # Excludes venv/
```

---

### Exercise 1.2: Recreate an Environment

**Scenario:**
Your teammate shared a project with this `requirements.txt`:
```
Django==4.2.5
Pillow==10.0.0
djangorestframework==3.14.0
```

**Task:**
1. Create a new virtual environment
2. Install all dependencies from the file
3. List installed packages to verify

**Expected Packages:**
- Django 4.2.5
- Pillow 10.0.0
- djangorestframework 3.14.0
- All their dependencies

---

### Exercise 1.3: Multiple Virtual Environments

**Task:**
Create two separate projects with different Django versions:

**Project A:**
- Folder: `legacy_project`
- Django: 3.2
- Python: 3.8+

**Project B:**
- Folder: `modern_project`
- Django: 4.2
- Python: 3.10+

**Verify:**
Both projects can run simultaneously with different Django versions.

---

## 🎓 Key Takeaways

1. ✅ Virtual environments isolate project dependencies
2. ✅ Always create a venv before installing Django
3. ✅ Use `requirements.txt` to track dependencies
4. ✅ Add `venv/` to `.gitignore`
5. ✅ Activate the environment before working on the project

---

## 🔗 Additional Resources

- [Python venv documentation](https://docs.python.org/3/library/venv.html)
- [Django installation guide](https://docs.djangoproject.com/en/4.2/topics/install/)
- [pip documentation](https://pip.pypa.io/en/stable/)

---

## 📚 Next Steps

Now that you have Django installed, let's create your first project!

[← Back to Part 1](./README.md) | [Next: Django-Admin & Project Creation →](./02-django-admin.md)
