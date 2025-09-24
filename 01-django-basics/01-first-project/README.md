# 🎯 Tutorial 1: Your First Django Project

**Level**: Beginner  
**Time**: 30-45 minutes  
**Prerequisites**: Python 3.8+ installed  

## 🎯 What You'll Build

In this tutorial, you'll create your first Django web application - a simple "Hello World" project that displays a personalized greeting page. You'll learn the fundamentals of Django project structure and how to create your first view.

## 📋 Learning Objectives

By the end of this tutorial, you will:

- ✅ Understand Django project structure
- ✅ Create a Django project and app
- ✅ Write your first view and URL pattern
- ✅ Run the Django development server
- ✅ Handle HTTP requests and responses

## 🚀 Step-by-Step Guide

### Step 1: Set Up Your Environment

First, create a virtual environment and install Django:

```bash
# Create virtual environment
python -m venv django_env

# Activate it (Windows)
django_env\Scripts\activate

# Activate it (Linux/Mac)
source django_env/bin/activate

# Install Django
pip install django==4.2.7
```

### Step 2: Create Your First Django Project

```bash
# Create a new Django project
django-admin startproject mysite

# Navigate to project directory
cd mysite

# Verify installation by running the server
python manage.py runserver
```

**🎉 Success!** You should see the Django welcome page at `http://127.0.0.1:8000/`

### Step 3: Understand Project Structure

Your project structure should look like this:

```
mysite/
├── manage.py          # Command-line utility for Django
├── mysite/
│   ├── __init__.py    # Makes Python treat directory as package
│   ├── settings.py    # Configuration for this Django project
│   ├── urls.py        # URL declarations for this project
│   ├── asgi.py        # ASGI config for deployment
│   └── wsgi.py        # WSGI config for deployment
```

### Step 4: Create Your First App

Django projects consist of multiple apps. Let's create one:

```bash
# Create a new app called 'hello'
python manage.py startapp hello
```

New structure:
```
mysite/
├── manage.py
├── hello/              # New app directory
│   ├── __init__.py
│   ├── admin.py        # Admin interface configuration
│   ├── apps.py         # App configuration
│   ├── models.py       # Database models
│   ├── tests.py        # Tests for your app
│   ├── views.py        # View functions
│   └── migrations/     # Database migrations
├── mysite/
│   └── ... (same as before)
```

### Step 5: Create Your First View

Edit `hello/views.py`:

```python
from django.http import HttpResponse
from django.shortcuts import render
import datetime

def hello_world(request):
    """Simple hello world view"""
    return HttpResponse("Hello, World! Welcome to Django! 🚀")

def hello_name(request, name):
    """Personalized greeting view"""
    current_time = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")
    message = f"""
    <html>
        <head>
            <title>Hello {name}!</title>
            <style>
                body {{ 
                    font-family: Arial, sans-serif; 
                    text-align: center; 
                    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
                    color: white;
                    padding: 50px;
                }}
                .container {{ 
                    background: rgba(255,255,255,0.1);
                    padding: 30px;
                    border-radius: 15px;
                    max-width: 600px;
                    margin: 0 auto;
                }}
                h1 {{ color: #fff; margin-bottom: 20px; }}
                p {{ font-size: 18px; line-height: 1.6; }}
                .time {{ 
                    background: rgba(255,255,255,0.2);
                    padding: 10px;
                    border-radius: 5px;
                    margin-top: 20px;
                }}
            </style>
        </head>
        <body>
            <div class="container">
                <h1>🎉 Hello, {name}!</h1>
                <p>Welcome to your first Django application!</p>
                <p>You've successfully created a dynamic web page with Django.</p>
                <div class="time">
                    <strong>Current time:</strong> {current_time}
                </div>
            </div>
        </body>
    </html>
    """
    return HttpResponse(message)
```

### Step 6: Configure URLs

Create `hello/urls.py`:

```python
from django.urls import path
from . import views

urlpatterns = [
    path('', views.hello_world, name='hello_world'),
    path('hello/<str:name>/', views.hello_name, name='hello_name'),
]
```

Update `mysite/urls.py`:

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('hello/', include('hello.urls')),
    path('', include('hello.urls')),  # Root URL
]
```

### Step 7: Test Your Application

```bash
# Run the development server
python manage.py runserver
```

Now visit these URLs:
- `http://127.0.0.1:8000/` - Basic hello world
- `http://127.0.0.1:8000/hello/YourName/` - Personalized greeting

## 🎊 What You've Learned

Congratulations! You've just:

1. ✅ **Created** your first Django project
2. ✅ **Built** a Django app with multiple views
3. ✅ **Configured** URL routing
4. ✅ **Handled** HTTP requests and responses
5. ✅ **Generated** dynamic HTML content

## 🔍 Code Explanation

### Views (`hello/views.py`)
- **`hello_world`**: Simple view returning plain text
- **`hello_name`**: Dynamic view accepting URL parameters and returning formatted HTML

### URLs (`hello/urls.py` and `mysite/urls.py`)
- **URL patterns** map URLs to view functions
- **Path parameters** (`<str:name>`) capture parts of the URL
- **`include()`** allows modular URL configuration

## 🚀 Next Steps

Ready for more? Here's what to explore next:

1. **Templates**: Move HTML to separate template files
2. **Static Files**: Add CSS, JavaScript, and images
3. **Models**: Learn about database integration
4. **Forms**: Handle user input
5. **Admin Interface**: Explore Django's built-in admin

## 💡 Best Practices Learned

- **Project Structure**: Keep apps focused on specific functionality
- **URL Configuration**: Use meaningful URL patterns
- **Code Organization**: Separate views, URLs, and models
- **Virtual Environments**: Always use virtual environments for Python projects

## 🐛 Common Issues & Solutions

### Issue: "No module named django"
**Solution**: Make sure your virtual environment is activated and Django is installed.

### Issue: "Page not found (404)"
**Solution**: Check your URL patterns and ensure they match your requests.

### Issue: Server won't start
**Solution**: Make sure no other process is using port 8000, or specify a different port:
```bash
python manage.py runserver 8080
```

## 📚 Additional Resources

- [Django Documentation](https://docs.djangoproject.com/)
- [Django Tutorial (Official)](https://docs.djangoproject.com/en/4.2/intro/tutorial01/)
- [Django Best Practices](https://django-best-practices.readthedocs.io/)

## 🏁 Challenge Exercise

Try extending this tutorial by:

1. Adding a view that displays the current date and time
2. Creating a view that shows a list of your favorite programming languages
3. Adding error handling for invalid names
4. Styling the pages with better CSS

**Share your solutions** by creating a pull request to this repository!

---

**Next Tutorial**: [02 - Models and Views](../02-models-views/) →

---

🎯 **Tutorial Complete!** Give yourself a pat on the back - you've just built your first Django application! 

**Questions?** Open an issue in this repository or start a discussion.