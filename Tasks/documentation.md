# Django Documentation

## Table of Contents
- [Introduction to Django](#introduction-to-django)
- [Key Features](#key-features)
- [MVT Architecture in Django](#mvt-architecture-in-django)
- [Installation Guide](#installation-guide)
- [Creating Your First Django Project](#creating-your-first-django-project)
- [Django App Structure](#django-app-structure)
- [Models](#models)
- [Views](#views)
- [Templates](#templates)
- [URLs](#urls)
- [Conclusion](#conclusion)
- [Resources](#resources)

---

## Introduction to Django
Django is a high-level Python web framework that enables rapid development of secure and maintainable websites. Instagram, Pinterest, The Washington Post, Spotify, Dropbox, Mozilla Support, Shopify, Prezi, NASA, and Disqus all use Django.

## Key Features
- **Object-Relational Mapping (ORM)**: Maps database tables to Python classes (models). Each model instance represents a row. Interact with your database using Python code instead of SQL.
- **Authentication System**: Provides a ready-to-use User model storing credentials, and handles secure password hashing and checking.
- **Admin Interface**:An auto-generated web-based UI for administrators to perform CRUD operations on database models.
- **Template Engine**: A language to embed dynamic logic (variables, loops, conditionals) into static HTML
- **URL Routing**: clean URL configuration to map specific URL patterns to their corresponding view functions.
- **Middleware**: A series of hooks that process all requests and responses globally before they reach the view or after they leave it.
- **REST Framework**: provides tools for serializing data, handling authentication, and creating flexible API endpoints.

## MVT Architecture in Django
Django follows a slightly modified MVC pattern called MTV:
- **Model**: The data access layer (database structure)
- **Template**: The presentation layer (how data is displayed)
- **View**: The business logic layer (what data to display)

## Installation Guide
### Prerequisites
- Python (3.6 or higher)
- pip (Python package installer)

### Steps
1. Create a virtual environment (recommended):
   ```bash
   python -m venv myenv
   source myenv\Scripts\activate
   ```
2. Install Django:
   ```bash
   pip install django
   ```
3. Verify installation:
   ```bash
   django-admin --version
   ```

## Creating Your First Django Project
```bash
django-admin startproject mysite
cd mysite
python manage.py runserver
```

## Django App Structure
```text
mysite/
    manage.py             - A command-line utility for running tasks like starting the server, applying migrations, creating apps, etc.
    mysite/
        __init__.py       - Marks this folder as a Python package.
        settings.py       - Central configuration file (databases, installed apps, middleware, templates, static files, etc.).
        urls.py           - it maps URLs to views.
        asgi.py           - Entry point for ASGI servers (used for asynchronous features like WebSockets).
        wsgi.py           - Entry point for WSGI servers (used for deploying Django on traditional web servers like Gunicorn, uWSGI, etc.).
    myapp/                - Each Django project can contain multiple apps. An app is a module focused on one specific functionality.
        __init__.py
        admin.py          - Register your models here so they appear in Django’s admin interface.
        apps.py           - Contains configuration for the app. Django uses this to recognize the app inside the project.
        models.py         - Defines database models (tables). Each model is a Python class.
        tests.py          - Place to write unit tests for the app.
        views.py          - Contains logic for handling requests and returning responses.
        migrations/       - Stores migration files that track changes to models and sync them with the database.
            __init__.py
```

## Models
This Django model defines a BlogPost with fields for the title, content, author (a link to a user), and timestamps for when it was created and last updated. It also includes a method to display the post's title in the admin interface.
This is a two-step process to manage changes to your database schema using Django's migration system.
#### 1. Create Migrations
Scans your Django project for any model changes (e.g., adding a new field, deleting a model) and packages these changes into a migration file.
#### 2. Apply Migrations
Applies the changes from the migration file(s) to your actual database, updating the schema to match your models.

## Views
### Function-Based View
FBVs are simple Python functions that take a request object as input and return a response.
### Class-Based View
CBVs use Python classes instead of functions. They are more structured and reusable.

## Templates
Templates in Django are HTML files that allow you to dynamically display data passed from views using its own template engine called Django Template Language (DTL).

## URLs
Django uses a concept called URL dispatcher to map incoming requests to the correct view function or class.
### Project URLs (mysite/urls.py)
```python
urlpatterns = [
    path('admin/', admin.site.urls),   #Connects to Django’s built-in admin panel.
    path('blog/', include('myapp.urls')),   #Delegates /blog/ related routes to the myapp/urls.py file.
]
```

### Django's Perceived Pros & Cons

| Aspect | Strengths | Limitations |
| :--- | :--- | :--- |
| **Features & Productivity** | Built-in admin, ORM, auth, migrations—rapid development | Heavyweight, steeper learning curve |
| **Documentation & Community** | Excellent guides, large community support | — |
| **Migrations** | Automated and reliable model syncing | — |
| **Admin Interface** | Instant CRUD interface for prototyping and management | — |
| **Scalability** | Used successfully by large sites (Instagram, Disqus) | — |
| **Performance** | Adequate for complex apps; optimizable with caching & tuning | Slower than async-first frameworks like FastAPI |
| **Flexibility** | Great for structured applications | Less flexible for unconventional / lightweight use-cases |
| **ORM & Advanced Queries** | Easy to use | ORM not ideal for complex analytical queries |
| **Team Onboarding** | Good defaults & structure aid collaboration | — |

## Conclusion
Django is a powerful, versatile framework that simplifies web development. Its "batteries-included" approach helps you build secure and scalable applications quickly.

## Resources
- [Official Django Docs](https://docs.djangoproject.com/)
- [Django REST Framework](https://www.django-rest-framework.org/)